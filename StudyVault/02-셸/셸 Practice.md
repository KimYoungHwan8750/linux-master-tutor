---
source_pdf: programjy.tistory.com
part: "Part2 Ch02"
keywords: practice, shell, env-var, config-file
---

# 셸 Practice (10문제)

#practice #shell

## 관련 개념
- [[셸의 종류와 특징]]
- [[셸 환경설정]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | POSIX 호환, GNU, 리눅스 기본셸 | bash (/bin/bash) |
> | C 언어 문법, UC Berkeley, Bill Joy | csh (/bin/csh) |
> | 히스토리/별칭 최초 도입 | csh |
> | PS1의 \u, \h, \w | 사용자, 호스트, 작업디렉토리 |
> | 시스템 전체 + 로그인 시 | /etc/profile |
> | 셸 변수 → 환경변수 | export |
> | 로그인 셸 변경 | chsh -s |

---

## 문제 1 - 셸 식별 [recall]
> 다음 설명에 해당하는 셸은?
>
> "GNU 프로젝트에서 개발되었으며, **Bourne Again Shell**의 약자이다. **POSIX 호환**을 지원하고, 대부분의 리눅스 배포판에서 **기본 셸**로 사용된다."

> [!answer]- 정답 보기
> **배쉬셸 (bash, /bin/bash)**
> - Brian Fox가 GNU 프로젝트에서 개발
> - POSIX 표준 호환
> - 본셸의 기능을 포함하면서 히스토리, 별칭, 자동완성 등 다양한 기능 제공

---

## 문제 2 - 셸 계열 구분 [recall]
> 다음 셸들을 **본셸 계열**과 **C셸 계열**로 분류하시오.
>
> sh, csh, ksh, tcsh, bash, zsh

> [!answer]- 정답 보기
> | 본셸 계열 | C셸 계열 |
> |----------|---------|
> | **sh** (본셸) | **csh** (C셸) |
> | **ksh** (콘셸) | **tcsh** (tc셸) |
> | **bash** (배쉬셸) | |
> | **zsh** (지셸) | |
>
> - 본셸 계열: sh에서 파생, Bourne 문법
> - C셸 계열: C 언어 문법 기반, Bill Joy가 UC Berkeley에서 개발

---

## 문제 3 - PS1 특수문자 [application]
> 다음과 같은 프롬프트를 표시하려면 PS1을 어떻게 설정해야 하는가?
>
> 출력: `june@myserver ~/projects$`
> (사용자명@호스트명 작업디렉토리$)

> [!answer]- 정답 보기
> ```bash
> PS1='\u@\h \w\$ '
> ```
> - `\u`: 사용자명 (june)
> - `\h`: 호스트명 (myserver)
> - `\w`: 현재 작업 디렉토리 (~/projects)
> - `\$`: 프롬프트 기호 (일반=$, root=#)

---

## 문제 4 - 설정 파일 적용 범위 [recall]
> 다음 설정 파일을 **적용 범위**와 **적용 시점**으로 분류하시오.
>
> ① /etc/profile
> ② ~/.bashrc
> ③ /etc/bashrc
> ④ ~/.bash_profile

> [!answer]- 정답 보기
> | 설정 파일 | 적용 범위 | 적용 시점 |
> |-----------|----------|----------|
> | ① /etc/profile | **시스템 전체** | **로그인 시** |
> | ② ~/.bashrc | **개인** | **bash 실행 시** |
> | ③ /etc/bashrc | **시스템 전체** | **bash 실행 시** |
> | ④ ~/.bash_profile | **개인** | **로그인 시** |

---

## 문제 5 - 환경변수 명령어 [recall]
> 다음 중 **셸 변수를 환경변수로 전환**하여 자식 프로세스에서도 사용할 수 있게 하는 명령어는?
>
> ① env
> ② set
> ③ export
> ④ printenv

> [!answer]- 정답 보기
> **③ export**
> - `export VAR=value`: 셸 변수를 환경변수로 전환
> - env/printenv: 환경변수 목록 **표시**
> - set: 셸 변수 + 환경변수 모두 **표시**

---

## 문제 6 - /etc/passwd 분석 [analysis]
> 다음 /etc/passwd 항목을 분석하시오.
>
> ```
> june:x:1000:1000:June User:/home/june:/bin/zsh
> ```
> 각 필드의 의미를 설명하고, 이 사용자의 기본 셸을 bash로 변경하는 명령어를 작성하시오.

> [!answer]- 정답 보기
> | 필드 | 값 | 의미 |
> |------|-----|------|
> | 1 | june | 사용자명 |
> | 2 | x | 비밀번호 (/etc/shadow에 저장) |
> | 3 | 1000 | UID (사용자 ID) |
> | 4 | 1000 | GID (기본 그룹 ID) |
> | 5 | June User | 설명 (GECOS) |
> | 6 | /home/june | 홈 디렉토리 |
> | 7 | /bin/zsh | 로그인 셸 |
>
> 셸 변경 명령어:
> ```bash
> chsh -s /bin/bash june
> # 또는
> usermod -s /bin/bash june
> ```

---

## 문제 7 - history 명령어 [application]
> 다음 중 **직전에 실행한 명령어를 다시 실행**하는 방법은?
>
> ① history -1
> ② !-1
> ③ !!
> ④ !$

> [!answer]- 정답 보기
> **③ !!**
> - `!!`: 직전 명령어 재실행
> - `!n`: n번 히스토리 명령어 재실행
> - `!문자열`: 해당 문자열로 시작하는 최근 명령어 재실행
> - `!$`: 직전 명령어의 마지막 인자

---

## 문제 8 - 환경변수 식별 [recall]
> 다음 환경변수와 그 설명을 올바르게 연결하시오.
>
> A. PATH &nbsp;&nbsp;&nbsp; B. HISTFILE &nbsp;&nbsp;&nbsp; C. PS2 &nbsp;&nbsp;&nbsp; D. DISPLAY
>
> ① 명령어 히스토리 저장 파일 경로
> ② X 윈도우 디스플레이 서버 지정
> ③ 명령어 검색 경로
> ④ 보조 프롬프트 (명령행 연속)

> [!answer]- 정답 보기
> - A-③: **PATH** = 명령어 검색 경로
> - B-①: **HISTFILE** = 히스토리 저장 파일 경로 (~/.bash_history)
> - C-④: **PS2** = 보조 프롬프트 (명령이 다음 줄로 이어질 때 표시, 기본값 >)
> - D-②: **DISPLAY** = X 윈도우 디스플레이 서버

---

## 문제 9 - alias 설정 [application]
> `ls -al` 명령어를 `ll`이라는 별칭으로 설정하고, 이 설정을 **영구적으로** 유지하려면 어떻게 해야 하는가?

> [!answer]- 정답 보기
> ```bash
> # 1. 현재 세션에서 별칭 설정
> alias ll='ls -al'
>
> # 2. 영구 설정을 위해 ~/.bashrc에 추가
> echo "alias ll='ls -al'" >> ~/.bashrc
>
> # 3. 변경사항 즉시 적용
> source ~/.bashrc
> ```
> - alias는 현재 세션에서만 유효하므로 **~/.bashrc**에 추가해야 영구적으로 유지된다
> - `source` 또는 `.` 명령어로 설정 파일을 즉시 적용할 수 있다

---

## 문제 10 - 셸 개발자 매칭 [analysis]
> 다음 셸과 개발자/개발 기관을 올바르게 연결하시오.
>
> | 셸 | 개발자/기관 |
> |----|-----------|
> | ① sh | A. David Korn, AT&T Bell Labs |
> | ② csh | B. Brian Fox, GNU 프로젝트 |
> | ③ ksh | C. Stephen Bourne, Bell Labs |
> | ④ bash | D. Bill Joy, UC Berkeley |

> [!answer]- 정답 보기
> | 셸 | 개발자/기관 |
> |----|-----------|
> | ① sh | **C. Stephen Bourne, Bell Labs** |
> | ② csh | **D. Bill Joy, UC Berkeley** |
> | ③ ksh | **A. David Korn, AT&T Bell Labs** |
> | ④ bash | **B. Brian Fox, GNU 프로젝트** |
>
> 기억법:
> - **B**ourne → **B**ell Labs
> - **C** Shell → **C** 언어 + UC **B**erkeley
> - **K**orn Shell → David **K**orn
> - **B**ash → **B**ourne **A**gain → GNU

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | POSIX 호환, GNU, 기본셸 | bash (/bin/bash) |
> | C 언어 문법, UC Berkeley | csh (/bin/csh) |
> | 본셸 계열 4종 | sh, ksh, bash, zsh |
> | C셸 계열 2종 | csh, tcsh |
> | PS1: \u, \h, \w, \$ | 사용자, 호스트, 디렉토리, 프롬프트 |
> | 시스템 전체 + 로그인 | /etc/profile |
> | 개인 + bash 실행 | ~/.bashrc |
> | 변수를 환경변수로 전환 | export |
> | 직전 명령어 재실행 | !! |
> | 셸 변경 명령어 | chsh -s 또는 usermod -s |
