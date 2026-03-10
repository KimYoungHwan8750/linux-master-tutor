---
source_pdf: programjy.tistory.com
part: "리눅스마스터 2급 2차 - 소프트웨어 설치 Practice"
keywords: practice, package-manager, rpm, dpkg, compression
---

# 소프트웨어 설치 Practice (10문제)

#practice #package-mgmt

## 관련 개념
- [[소프트웨어 설치 및 삭제]]
- [[파일시스템 관리 명령어]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | rpm 설치 (상세+진행) | `rpm -ivh` |
> | rpm 업그레이드 (없으면 설치) | `rpm -Uvh` |
> | rpm 이미 설치된 것만 업그레이드 | `rpm -Fvh` |
> | rpm 삭제 | `rpm -e` |
> | rpm 전체 목록 | `rpm -qa` |
> | dpkg 완전 삭제 | `dpkg -P` |
> | apt-get 목록 갱신 | `apt-get update` |
> | 소스 설치 순서 | tar → configure → make → make install |
> | 압축 효율 | xz > bz2 > gz > compress |
> | tar bzip2 옵션 | `-j` |

---

## 문제 1 - rpm 설치 옵션 [recall]
> `httpd-2.4.6.rpm` 패키지를 설치 진행 상황과 상세 정보를 출력하면서 설치하려고 한다. 올바른 명령어는?

> [!answer]- 정답 보기
> ```bash
> rpm -ivh httpd-2.4.6.rpm
> ```
> **해설**: `-i`는 설치(install), `-v`는 상세정보(verbose), `-h`는 설치 진행률을 해시(#)로 표시한다.

---

## 문제 2 - rpm 업그레이드 구분 [recall]
> rpm의 `-U`와 `-F` 옵션의 차이점을 서술하시오.

> [!answer]- 정답 보기
> - **`-U` (Upgrade)**: 패키지가 설치되어 있으면 업그레이드, **설치되어 있지 않으면 새로 설치**
> - **`-F` (Freshen)**: 패키지가 **이미 설치되어 있는 경우에만** 업그레이드, 설치되어 있지 않으면 아무 동작 안 함
>
> 핵심 차이: `-U`는 미설치 시에도 설치 진행, `-F`는 미설치 시 무시

---

## 문제 3 - rpm 질의 [recall]
> 현재 시스템에 설치된 모든 rpm 패키지의 목록을 확인하는 명령어는?

> [!answer]- 정답 보기
> ```bash
> rpm -qa
> ```
> **해설**: `-q`는 질의(query), `-a`는 전체(all). 특정 패키지를 찾으려면 `rpm -qa | grep httpd`와 같이 사용할 수 있다.

---

## 문제 4 - dpkg 삭제 옵션 [recall]
> Debian 계열에서 `apache2` 패키지를 설정 파일까지 포함하여 완전히 삭제하려면 어떤 명령어를 사용해야 하는가?

> [!answer]- 정답 보기
> ```bash
> dpkg -P apache2
> ```
> **해설**: `-P`는 Purge의 약자로, 패키지 파일과 **설정 파일까지 모두 삭제**한다. `-r`(remove)은 설정 파일을 남기고 삭제한다.

---

## 문제 5 - 소스 설치 순서 [application]
> 소스 코드를 다운로드하여 리눅스에 소프트웨어를 설치하려고 한다. 다음 빈칸 (가)~(다)에 들어갈 명령어를 순서대로 적으시오.
> ```
> tar xvzf program.tar.gz
> cd program
> (가)
> (나)
> (다)
> ```

> [!answer]- 정답 보기
> - **(가)**: `./configure` — 시스템 환경을 검사하고 **Makefile**을 생성
> - **(나)**: `make` — Makefile을 기반으로 소스 코드를 **컴파일**
> - **(다)**: `make install` — 컴파일된 바이너리를 시스템에 **설치**
>
> 전체 순서: `tar` → `./configure` → `make` → `make install` → (`make clean`)

---

## 문제 6 - 압축 효율성 [recall]
> 다음 압축 도구를 압축 효율이 높은 순서대로 나열하시오.
> `gzip, xz, compress, bzip2`

> [!answer]- 정답 보기
> **xz > bzip2 > gzip > compress**
>
> | 순위 | 도구 | 확장자 | tar 옵션 |
> |------|------|--------|----------|
> | 1 (최고) | xz | .xz | `-J` |
> | 2 | bzip2 | .bz2 | `-j` |
> | 3 | gzip | .gz | `-z` |
> | 4 (최저) | compress | .Z | `-Z` |

---

## 문제 7 - tar 압축 옵션 [application]
> `/home/user/project` 디렉터리를 bzip2로 압축하여 `project.tar.bz2` 파일로 만드는 tar 명령어를 작성하시오.

> [!answer]- 정답 보기
> ```bash
> tar cvjf project.tar.bz2 /home/user/project
> ```
> **해설**: `-c`(생성), `-v`(상세), `-j`(**bzip2** 압축), `-f`(파일명 지정). bzip2는 소문자 `-j`, xz는 대문자 `-J`임에 주의.

---

## 문제 8 - 온라인 vs 오프라인 패키지 관리 [analysis]
> Red Hat 계열에서 `yum install httpd`와 `rpm -ivh httpd.rpm`의 차이점을 설명하고, 어떤 상황에서 각각을 사용하는 것이 적절한지 서술하시오.

> [!answer]- 정답 보기
> | 구분 | yum | rpm |
> |------|-----|-----|
> | 패키지 소스 | 인터넷 저장소(Repository) | 로컬 파일 |
> | 의존성 해결 | **자동** | **수동** (의존성 오류 시 직접 해결) |
> | 네트워크 필요 | O | X |
>
> - **yum**: 인터넷 연결이 가능하고, 의존성이 복잡한 패키지를 편리하게 설치할 때
> - **rpm**: 인터넷이 없는 환경이거나, 특정 버전의 .rpm 파일을 직접 설치해야 할 때

---

## 문제 9 - apt-get 명령어 구분 [analysis]
> 다음 apt-get 명령어의 차이를 설명하시오.
> (1) `apt-get update`
> (2) `apt-get upgrade`
> (3) `apt-get dist-upgrade`

> [!answer]- 정답 보기
> | 명령어 | 역할 |
> |--------|------|
> | `apt-get update` | 저장소에서 **패키지 목록(인덱스)**을 최신으로 갱신. 실제 패키지를 설치/업그레이드하지 않음 |
> | `apt-get upgrade` | 설치된 패키지를 **최신 버전으로 업그레이드**. 새 패키지 추가/기존 패키지 삭제는 하지 않음 |
> | `apt-get dist-upgrade` | 의존성 변경을 고려하여 **패키지 추가/삭제**까지 수행하는 전체 업그레이드 |
>
> 일반적인 사용 순서: `update` → `upgrade` 또는 `update` → `dist-upgrade`

---

## 문제 10 - configure의 역할 [recall]
> 소스 코드 설치 과정에서 `./configure` 명령어의 주된 역할 두 가지를 서술하시오.

> [!answer]- 정답 보기
> 1. **시스템 환경 검사**: 컴파일에 필요한 라이브러리, 헤더 파일, 컴파일러 등이 시스템에 존재하는지 확인
> 2. **Makefile 생성**: 시스템 환경에 맞는 **Makefile**을 자동으로 생성하여, 이후 `make` 명령에서 사용할 수 있도록 함
>
> `--prefix` 옵션으로 설치 경로를 지정할 수 있다. (예: `./configure --prefix=/usr/local`)

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | rpm 설치 상세+진행 | `rpm -ivh` |
> | rpm -U vs -F | -U: 미설치시 설치 / -F: 미설치시 무시 |
> | rpm 전체 목록 | `rpm -qa` |
> | rpm 삭제 | `rpm -e` |
> | dpkg 완전 삭제 | `dpkg -P` (Purge) |
> | dpkg 파일 목록 | `dpkg -L` |
> | 소스 설치 순서 | tar → configure → make → make install |
> | configure 역할 | 환경검사 + Makefile 생성 |
> | 압축 효율 순서 | xz > bz2 > gz > compress |
> | tar bzip2/xz 옵션 | `-j` / `-J` |
> | apt-get update vs upgrade | update: 목록갱신 / upgrade: 패키지 업그레이드 |
> | yum vs rpm | yum: 온라인+의존성자동 / rpm: 오프라인+수동 |
