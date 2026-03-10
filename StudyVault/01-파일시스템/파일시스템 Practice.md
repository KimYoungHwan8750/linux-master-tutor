---
source_pdf: programjy.tistory.com
part: "Part2 Ch01"
keywords: practice, permission, quota, mount, filesystem
---

# 파일시스템 Practice (12문제)

#practice #filesystem

## 관련 개념
- [[파일 권한과 소유권]]
- [[디스크 쿼타와 파일시스템]]
- [[파일시스템 관리 명령어]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | umask 022 → 파일 기본 권한 | 644 |
> | SetUID 설정된 rwsr-xr-x | 4755 |
> | /tmp 특수 권한 | Sticky Bit (1777) |
> | 편집기로 쿼터 설정 | edquota |
> | XFS 쿼터 관리 | xfs_quota -x -c |
> | 부팅 시 자동 마운트 설정 | /etc/fstab |
> | ISO 이미지 마운트 | mount -o loop |
> | 디스크 사용량 요약 | du -sh |

---

## 문제 1 - umask와 기본 권한 [recall]
> umask 값이 `027`로 설정되어 있을 때, 새로 생성되는 **파일**과 **디렉토리**의 기본 권한은 각각 무엇인가?

> [!answer]- 정답 보기
> **파일**: 666 - 027 = **640** (rw-r-----)
> **디렉토리**: 777 - 027 = **750** (rwxr-x---)
>
> 파일의 기본 최대 권한은 666(실행권한 없음), 디렉토리는 777이다.
> umask 값을 빼면 실제 부여되는 권한이 된다.

---

## 문제 2 - 특수 권한 식별 [recall]
> 다음 파일의 허가권을 8진수로 표현하시오.
> ```
> -rwsr-xr-t 1 root root 12345 Oct 1 test_file
> ```

> [!answer]- 정답 보기
> **5755**
> - SetUID (s가 소유자 실행 위치) → **4**000
> - Sticky Bit (t가 기타 실행 위치) → **1**000
> - 특수 권한: 4 + 1 = **5**
> - 소유자: rwx = **7**, 그룹: r-x = **5**, 기타: r-x(t) = **5**
> - 최종: **5755**

---

## 문제 3 - chown 명령어 [application]
> `/data` 디렉토리와 그 하위 모든 파일의 소유자를 `admin`, 그룹을 `staff`로 변경하는 명령어를 작성하시오.

> [!answer]- 정답 보기
> ```bash
> chown -R admin:staff /data
> ```
> - `-R`: 재귀적으로 하위 디렉토리와 파일 모두 적용
> - `admin:staff`: 소유자를 admin, 그룹을 staff로 변경
> - chown은 소유자와 그룹을 동시에 변경할 수 있다 (`:` 또는 `.`으로 구분)

---

## 문제 4 - edquota vs setquota [recall]
> 다음 중 디스크 쿼터 설정 명령어에 대한 설명으로 **틀린 것**은?
>
> ① edquota는 vi 편집기를 이용하여 쿼터를 설정한다
> ② setquota는 명령행에서 직접 쿼터 값을 입력한다
> ③ edquota -t는 유예 기간(grace period)을 설정한다
> ④ setquota는 편집기를 사용하므로 스크립트 자동화에 적합하다

> [!answer]- 정답 보기
> **④**
> setquota는 **편집기를 사용하지 않고** 명령행에서 직접 값을 입력하므로 스크립트 자동화에 적합하다.
> 편집기를 사용하는 것은 **edquota**이다.

---

## 문제 5 - /etc/fstab 분석 [analysis]
> 다음 /etc/fstab 항목을 분석하시오.
> ```
> UUID=a1b2c3d4  /home  ext4  defaults,usrquota  1  2
> ```
> 각 필드의 의미를 설명하시오.

> [!answer]- 정답 보기
> | 필드 | 값 | 의미 |
> |------|-----|------|
> | 1 | UUID=a1b2c3d4 | 장치 식별자 (UUID) |
> | 2 | /home | 마운트 포인트 |
> | 3 | ext4 | 파일시스템 유형 |
> | 4 | defaults,usrquota | 마운트 옵션 (기본값 + 사용자 쿼터 활성화) |
> | 5 | 1 | dump 백업 사용 (1=활성화) |
> | 6 | 2 | fsck 점검 순서 (2=루트 이후에 점검) |

---

## 문제 6 - 파일시스템 종류 [recall]
> 다음 설명에 해당하는 파일시스템은?
>
> "ext2를 개선하여 **저널링**과 **ACL**을 지원하며, ext2와 호환성을 유지한다."

> [!answer]- 정답 보기
> **ext3**
> - ext3는 ext2에 저널링(Journaling)과 ACL(Access Control List)을 추가한 파일시스템
> - ext2와 하위 호환성을 유지하므로 ext2에서 ext3로 변환 가능
> - 저널링: 비정상 종료 시 저널 로그를 이용해 빠르고 안정적인 복구 가능

---

## 문제 7 - mount 명령어 [application]
> CD-ROM의 ISO 이미지 파일 `centos7.iso`를 `/mnt/cdrom` 디렉토리에 마운트하는 명령어를 작성하시오.

> [!answer]- 정답 보기
> ```bash
> mount -o loop centos7.iso /mnt/cdrom
> ```
> - `-o loop`: ISO 이미지 파일을 마운트할 때 반드시 사용하는 옵션
> - loop 장치를 통해 파일을 블록 장치처럼 취급하여 마운트

---

## 문제 8 - du vs df [recall]
> 다음 중 **디스크 여유 공간**을 사람이 읽기 쉬운 단위로 확인하면서 **파일시스템 유형**도 함께 표시하는 명령어는?
>
> ① `du -sh`
> ② `df -hT`
> ③ `du -hT`
> ④ `df -si`

> [!answer]- 정답 보기
> **②** `df -hT`
> - df: 디스크 **여유 공간** 확인 (du는 사용량)
> - -h: 사람이 읽기 쉬운 단위 (human-readable)
> - -T: 파일시스템 유형(Type) 표시

---

## 문제 9 - 네트워크 파일시스템 [recall]
> 다음 설명에 해당하는 네트워크 파일시스템 프로토콜은?
>
> "**윈도우와 리눅스** 간에 파일과 프린터를 공유하기 위한 프로토콜로, **삼바(Samba)**를 사용하여 구현한다."

> [!answer]- 정답 보기
> **SMB (Server Message Block)**
> - SMB는 Microsoft가 개발한 파일/프린터 공유 프로토콜
> - 리눅스에서는 삼바(Samba)를 사용하여 SMB 프로토콜을 구현
> - CIFS는 SMB를 확장/개선한 프로토콜
> - NFS는 리눅스/유닉스 간 파일 공유 (구분 주의)

---

## 문제 10 - fdisk 대화형 명령 [application]
> fdisk 대화형 모드에서 새 파티션을 생성하고 변경 사항을 저장하여 종료하려면 어떤 내부 명령어를 순서대로 사용해야 하는가?

> [!answer]- 정답 보기
> **n** → **w**
> - `n` (new): 새 파티션 생성
> - `w` (write): 변경 사항을 디스크에 저장하고 종료
> - 참고: `q`는 저장 없이 종료, `p`는 파티션 테이블 출력, `d`는 삭제

---

## 문제 11 - xfs_quota [application]
> CentOS 7 서버에서 XFS 파일시스템의 /home 파티션에 대해 사용자 `june`의 블록 소프트 제한을 100MB, 하드 제한을 200MB로 설정하는 명령어를 작성하시오.

> [!answer]- 정답 보기
> ```bash
> xfs_quota -x -c 'limit bsoft=100m bhard=200m june' /home
> ```
> - `-x`: 전문가(expert) 모드 활성화
> - `-c '명령'`: 실행할 쿼터 명령 지정
> - `limit bsoft=100m bhard=200m june`: 사용자 june의 블록 소프트/하드 제한 설정
> - CentOS 7에서는 기본 파일시스템이 XFS이므로 xfs_quota를 사용

---

## 문제 12 - 종합 분석 [analysis]
> 다음 상황을 분석하고 해결 명령어를 제시하시오.
>
> 시스템 관리자가 `/dev/sdb1` 파티션을 ext4로 포맷한 후 `/data`에 마운트하고, 부팅 시 자동 마운트되도록 설정하려 한다. 또한 이 파티션에 사용자 쿼터를 활성화하려 한다. 필요한 절차를 순서대로 나열하시오.

> [!answer]- 정답 보기
> ```bash
> # 1. 파일시스템 생성 (포맷)
> mkfs -t ext4 /dev/sdb1
>
> # 2. 마운트 포인트 생성
> mkdir /data
>
> # 3. 마운트
> mount -t ext4 /dev/sdb1 /data
>
> # 4. /etc/fstab에 자동 마운트 및 쿼터 설정 추가
> # /dev/sdb1  /data  ext4  defaults,usrquota  1  2
>
> # 5. 재마운트 (fstab 옵션 적용)
> mount -o remount /data
>
> # 6. 쿼터 파일 생성
> quotacheck -augm
>
> # 7. 쿼터 활성화
> quotaon -a
>
> # 8. 개별 사용자 쿼터 설정
> edquota 사용자명
> ```

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | umask 027 → 파일 | 640 (rw-r-----) |
> | SetUID + Sticky Bit + 755 | 5755 |
> | 소유자+그룹 재귀 변경 | chown -R 소유자:그룹 |
> | 편집기 쿼터 vs 명령행 쿼터 | edquota vs setquota |
> | fstab 6번째 필드 | fsck 점검 순서 |
> | ext2 + 저널링 + ACL | ext3 |
> | ISO 이미지 마운트 | mount -o loop |
> | 여유공간 + 타입 | df -hT |
> | 윈도우-리눅스 파일 공유 | SMB (삼바) |
> | fdisk 저장 종료 | w |
> | XFS 쿼터 관리 | xfs_quota -x -c |
> | 파일시스템 포맷 | mkfs -t ext4 |
