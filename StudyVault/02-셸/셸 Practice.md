---
source_pdf: 원문 미보유 (웹 소스)
part: Part 2 Ch02
keywords: practice, shell, bash, environment
---

# 셸 Practice (10 questions)

#practice #shell

## Related Concepts
- [[셸의 종류와 특징]]
- [[셸 환경설정]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | 리눅스 기본 셸 | bash |
> | C언어 기반 셸 | csh |
> | 셸 변경 | chsh |
> | 전체 사용자 환경변수 | /etc/profile |
> | 개인 alias | ~/.bashrc |

---

## Question 1 - 셸 계열 분류 [recall]
> bash, ksh, csh, tcsh 중 본셸 계열에 해당하는 것은?

> [!answer]- 정답 보기
> **bash, ksh** — 본셸 계열. csh와 tcsh는 C셸 계열.

---

## Question 2 - 기본 셸 확인 [recall]
> 현재 사용 중인 로그인 셸을 확인하는 명령은?

> [!answer]- 정답 보기
> `echo $SHELL` — 환경변수 SHELL에 현재 로그인 셸 경로가 저장됨

---

## Question 3 - 셸 변경 [recall]
> 사용자의 로그인 셸을 변경하는 명령어는?

> [!answer]- 정답 보기
> **chsh** — `chsh -s /bin/zsh`로 zsh 변경. `/etc/shells`에 등록된 셸만 변경 가능.

---

## Question 4 - 환경설정 파일 [recall]
> 모든 사용자에게 공통 환경변수를 설정하려면 어느 파일을 수정해야 하는가?

> [!answer]- 정답 보기
> **/etc/profile** — 전체 사용자에게 적용되는 환경변수 설정 파일

---

## Question 5 - history 기능 [recall]
> bash에서 직전에 실행한 명령을 다시 실행하는 방법은?

> [!answer]- 정답 보기
> **!!** — 직전 명령 재실행. `!N`은 N번째 명령 재실행.

---

## Question 6 - alias 설정 [recall]
> `alias rm='rm -i'`를 영구적으로 적용하려면 어느 파일에 추가해야 하는가?

> [!answer]- 정답 보기
> **~/.bashrc** — 개인 사용자의 비로그인 셸 설정 파일에 추가하면 영구 적용

---

## Question 7 - 환경변수 활용 [application]
> 새로운 프로그램을 `/opt/myapp/bin`에 설치했다. 어디서든 실행 가능하게 하려면?

> [!answer]- 정답 보기
> `export PATH=$PATH:/opt/myapp/bin`을 `~/.bash_profile` (개인) 또는 `/etc/profile` (전체)에 추가

---

## Question 8 - 설정 파일 로드 순서 [application]
> 사용자가 SSH로 로그인할 때 셸 설정 파일의 로드 순서는?

> [!answer]- 정답 보기
> `/etc/profile` → `~/.bash_profile` → `~/.bashrc` → `/etc/bashrc`
> SSH 로그인은 **로그인 셸**이므로 profile 계열부터 실행

---

## Question 9 - /etc/profile vs ~/.bashrc 비교 [analysis]
> `/etc/profile`과 `~/.bashrc`의 차이를 범위, 실행 시점, 용도 측면에서 비교하시오.

> [!answer]- 정답 보기
> | 항목 | /etc/profile | ~/.bashrc |
> |------|-------------|-----------|
> | 범위 | 전체 사용자 | 개인 |
> | 시점 | 로그인 셸 | 비로그인 셸 |
> | 용도 | 환경변수, PATH | alias, 함수 |

---

## Question 10 - 본셸 vs C셸 비교 [analysis]
> 본셸 계열과 C셸 계열의 대표적인 차이점을 문법과 기능 관점에서 비교하시오.

> [!answer]- 정답 보기
> | 항목 | 본셸 계열(sh/bash) | C셸 계열(csh/tcsh) |
> |------|-------------------|-------------------|
> | 문법 | sh 스크립트 문법 | C언어 유사 문법 |
> | 변수 설정 | `VAR=value` | `set VAR=value` |
> | 조건문 | `if-then-fi` | `if-then-endif` |
> | 리다이렉션 | `2>&1` | `>&` |
> | 대표 셸 | bash (리눅스 기본) | tcsh |

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | 리눅스 기본 셸 | bash |
> | 셸 변경 | chsh |
> | 전체 환경변수 | /etc/profile |
> | 개인 alias | ~/.bashrc |
> | 직전 명령 재실행 | !! |
