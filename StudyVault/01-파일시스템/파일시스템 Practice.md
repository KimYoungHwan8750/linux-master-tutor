---
source_pdf: 원문 미보유 (웹 소스)
part: Part 2 Ch01
keywords: practice, filesystem, permission, quota
---

# 파일시스템 Practice (10 questions)

#practice #filesystem

## Related Concepts
- [[파일 권한과 소유권]]
- [[디스크 쿼타와 파일시스템]]
- [[파일시스템 관리 명령어]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | chmod 숫자 4자리 | 특수권한 포함 |
> | r=4, w=2, x=1 | 권한 숫자 계산 |
> | SetUID=4000 | 소유자 실행 권한 |
> | /etc/fstab | 부팅 시 자동 마운트 |
> | edquota | 대화형 쿼타 편집 |

---

## Question 1 - chmod 숫자 변환 [recall]
> `rwxr-x---` 를 숫자로 표현하면?

> [!answer]- 정답 보기
> **750** — rwx(4+2+1=7) + r-x(4+0+1=5) + ---(0+0+0=0)

---

## Question 2 - 특수 권한 식별 [recall]
> `chmod 4755 file.sh` 실행 후 `ls -l`로 확인할 때 나타나는 권한 표시는?

> [!answer]- 정답 보기
> **-rwsr-xr-x** — 4000(SetUID)으로 소유자 x 위치가 `s`로 표시됨

---

## Question 3 - Sticky bit 적용 사례 [recall]
> `/tmp` 디렉토리에 Sticky bit가 설정된 이유는?

> [!answer]- 정답 보기
> 모든 사용자가 파일을 생성할 수 있지만, **자신의 파일만 삭제**할 수 있도록 하기 위해서. root와 파일 소유자만 삭제 가능.

---

## Question 4 - 소유권 변경 [recall]
> 파일의 소유자를 `admin`, 그룹을 `devteam`으로 동시에 변경하는 명령은?

> [!answer]- 정답 보기
> `chown admin:devteam filename` — 소유자와 그룹을 콜론으로 구분하여 동시 변경

---

## Question 5 - 파일시스템 종류 [recall]
> 리눅스에서 Windows와 파일을 공유할 때 사용하는 프로토콜은?

> [!answer]- 정답 보기
> **SMB/CIFS** — Windows 파일 공유 프로토콜. 리눅스 간 공유는 NFS 사용.

---

## Question 6 - 마운트 관련 [application]
> 새 하드디스크 `/dev/sdb`를 추가하여 `/data`에 ext4로 마운트하려 한다. 올바른 작업 순서는?

> [!answer]- 정답 보기
> 1. `fdisk /dev/sdb` — 파티션 생성
> 2. `mkfs -t ext4 /dev/sdb1` — 파일시스템 생성
> 3. `mkdir /data` — 마운트 포인트 생성
> 4. `mount -t ext4 /dev/sdb1 /data` — 마운트

---

## Question 7 - 쿼타 설정 [application]
> 사용자 `john`에게 디스크 쿼타를 설정하려 한다. soft limit 100MB, hard limit 200MB로 대화형 편집하는 명령은?

> [!answer]- 정답 보기
> `edquota john` — 대화형 에디터가 열리며 soft/hard limit을 직접 수정. CLI에서 직접 설정하려면 `setquota` 사용.

---

## Question 8 - fstab 해석 [application]
> `/etc/fstab`에 다음 항목이 있다: `/dev/sda2 /home ext4 defaults 1 2`. 각 필드의 의미는?

> [!answer]- 정답 보기
> 장치명(`/dev/sda2`) + 마운트포인트(`/home`) + 파일시스템(`ext4`) + 옵션(`defaults`) + 덤프 여부(`1`=백업) + fsck 순서(`2`)

---

## Question 9 - SetUID vs SetGID 분석 [analysis]
> SetUID와 SetGID의 차이를 설명하고, 각각이 보안에 미치는 영향을 비교하시오.

> [!answer]- 정답 보기
> - **SetUID**: 실행 시 파일 **소유자**의 권한으로 실행 (예: passwd 명령)
> - **SetGID**: 실행 시 파일 **그룹**의 권한으로 실행
> - 보안 영향: SetUID가 root 소유 파일에 설정되면 일반 사용자가 root 권한 획득 가능 → 보안 위험이 더 큼. 정기적으로 `find / -perm -4000`으로 점검 필요.

---

## Question 10 - 파일시스템 비교 [analysis]
> ext3, ext4, XFS 파일시스템의 특징을 비교하고, 대용량 서버에 적합한 파일시스템을 선택하시오.

> [!answer]- 정답 보기
> | 항목 | ext3 | ext4 | XFS |
> |------|------|------|-----|
> | 저널링 | O | O | O |
> | 최대 파일 | 2TB | 16TB | 8EB |
> | 최대 FS | 32TB | 1EB | 8EB |
> | 온라인 확장 | X | O | O |
>
> 대용량 서버에는 **XFS** 또는 **ext4** 추천. XFS는 대용량에 최적화, ext4는 범용성이 높음.

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | rwxr-xr-x 숫자 | 755 |
> | SetUID 숫자 | 4000 |
> | /tmp 보호 | Sticky bit |
> | 소유자+그룹 변경 | chown user:group |
> | 부팅 마운트 파일 | /etc/fstab |
> | 대화형 쿼타 | edquota |
