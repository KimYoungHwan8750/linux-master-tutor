---
source_pdf: 원문 미보유 (웹 소스)
part: Part 2 Ch05
keywords: practice, rpm, yum, apt, source install
---

# 소프트웨어설치 Practice (8 questions)

#practice #package

## Related Concepts
- [[소프트웨어 설치 및 삭제]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | RPM 설치 | rpm -ivh |
> | 의존성 해결 | YUM / APT-GET |
> | 소스 설치 순서 | configure → make → make install |
> | 최고 압축률 | xz |
> | tar gzip | -z 옵션 |

---

## Question 1 - RPM 설치 [recall]
> RPM 패키지를 설치하면서 진행률과 상세 정보를 표시하는 명령은?

> [!answer]- 정답 보기
> `rpm -ivh package.rpm` — i(설치) + v(상세) + h(진행률 #표시)

---

## Question 2 - YUM vs RPM [recall]
> YUM이 RPM에 비해 가장 큰 장점은?

> [!answer]- 정답 보기
> **의존성 자동 해결** — YUM은 필요한 의존 패키지를 자동으로 찾아 설치

---

## Question 3 - 소스 설치 순서 [recall]
> 소스 코드로 소프트웨어를 설치할 때의 3단계 순서는?

> [!answer]- 정답 보기
> `./configure` (환경 설정, Makefile 생성) → `make` (컴파일) → `make install` (설치)

---

## Question 4 - 압축 비교 [recall]
> gzip, bzip2, xz를 압축률 순서대로 나열하시오.

> [!answer]- 정답 보기
> **gzip < bzip2 < xz** — xz가 가장 높은 압축률, gzip이 가장 빠른 속도

---

## Question 5 - RPM 질의 [recall]
> 시스템에 설치된 모든 RPM 패키지 목록을 확인하는 명령은?

> [!answer]- 정답 보기
> `rpm -qa` — q(query) + a(all). 특정 패키지 검색: `rpm -qa | grep httpd`

---

## Question 6 - Debian 패키지 관리 [application]
> Debian 계열에서 패키지를 설정 파일까지 완전히 삭제하는 두 가지 방법은?

> [!answer]- 정답 보기
> 1. `dpkg -P package` — purge 옵션
> 2. `apt-get purge package`
> `apt-get remove`는 설정 파일이 남음!

---

## Question 7 - tar 옵션 활용 [application]
> `/home/backup` 디렉토리를 bzip2로 압축 아카이브하는 명령은?

> [!answer]- 정답 보기
> `tar cjvf backup.tar.bz2 /home/backup` — c(생성) + j(bzip2) + v(상세) + f(파일명)

---

## Question 8 - 패키지 관리 체계 비교 [analysis]
> RedHat 계열(RPM/YUM)과 Debian 계열(DPKG/APT)의 패키지 관리 체계를 비교하시오.

> [!answer]- 정답 보기
> | 항목 | RedHat 계열 | Debian 계열 |
> |------|------------|------------|
> | 로컬 관리 | RPM (.rpm) | DPKG (.deb) |
> | 온라인 관리 | YUM / DNF | APT-GET / APT |
> | 설정 위치 | /etc/yum.repos.d/ | /etc/apt/sources.list |
> | 설치 명령 | rpm -ivh | dpkg -i |
> | 의존성 해결 | YUM 사용 | APT 사용 |

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | RPM 설치 | rpm -ivh |
> | 의존성 해결 | YUM/APT-GET |
> | 소스 설치 | configure→make→make install |
> | 최고 압축률 | xz |
> | tar bzip2 | -j 옵션 |
> | 완전 삭제 | purge |
