---
source_pdf: 원문 미보유 (웹 소스)
part: Part 2 Ch03
keywords: practice, process, daemon, crontab
---

# 프로세스관리 Practice (10 questions)

#practice #process

## Related Concepts
- [[프로세스 관리]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | 강제 종료 시그널 | SIGKILL (9) |
> | 기본 종료 시그널 | SIGTERM (15) |
> | 우선순위 범위 | -20 ~ 19 |
> | 항상 상주 데몬 | standalone |
> | crontab 형식 | 분 시 일 월 요일 |

---

## Question 1 - kill 시그널 [recall]
> `kill` 명령의 기본 시그널 번호와 이름은?

> [!answer]- 정답 보기
> **15 (SIGTERM)** — 정상 종료 요청. 프로세스가 무시할 수 있음.

---

## Question 2 - 프로세스 확인 [recall]
> 시스템의 모든 프로세스를 풀포맷으로 확인하는 명령은?

> [!answer]- 정답 보기
> `ps -ef` 또는 `ps aux` — 전체 프로세스를 상세 정보와 함께 출력

---

## Question 3 - nice 값 범위 [recall]
> nice 값의 범위와, 값이 클수록 우선순위가 어떻게 되는지 설명하시오.

> [!answer]- 정답 보기
> 범위: **-20 ~ 19**. 값이 클수록 우선순위가 **낮아짐**. -20이 최고 우선순위.

---

## Question 4 - 데몬 방식 [recall]
> standalone 방식과 inetd(xinetd) 방식의 차이는?

> [!answer]- 정답 보기
> - **standalone**: 항상 메모리 상주, 빠른 응답, 리소스 많이 사용
> - **inetd**: 요청 시에만 실행, 리소스 절약, 응답 느림

---

## Question 5 - 백그라운드 실행 [recall]
> 명령어를 백그라운드로 실행하는 방법과, 로그아웃 후에도 계속 실행하는 방법은?

> [!answer]- 정답 보기
> - 백그라운드: `command &`
> - 로그아웃 후 유지: `nohup command &`

---

## Question 6 - crontab 해석 [recall]
> `30 2 * * 0 /backup.sh`의 의미는?

> [!answer]- 정답 보기
> **매주 일요일 새벽 2시 30분**에 /backup.sh 실행. (요일 0=일요일)

---

## Question 7 - crontab 작성 [application]
> 매주 월~금 오전 9시에 `/home/user/report.sh`를 실행하는 crontab 항목을 작성하시오.

> [!answer]- 정답 보기
> `0 9 * * 1-5 /home/user/report.sh` — 분(0) 시(9) 일(*) 월(*) 요일(1-5=월~금)

---

## Question 8 - 프로세스 제어 [application]
> 실행 중인 포그라운드 프로세스를 백그라운드로 전환하는 순서는?

> [!answer]- 정답 보기
> 1. `Ctrl+Z` — 프로세스 일시 정지
> 2. `bg %작업번호` — 백그라운드로 전환
> 다시 포그라운드로 가져오려면 `fg %작업번호`

---

## Question 9 - SIGKILL vs SIGTERM [analysis]
> SIGKILL(9)과 SIGTERM(15)의 차이를 설명하고, 각각 언제 사용해야 하는지 비교하시오.

> [!answer]- 정답 보기
> | 항목 | SIGTERM (15) | SIGKILL (9) |
> |------|-------------|-------------|
> | 처리 | 프로세스가 처리 가능 | 무시 불가 |
> | 정리 | 정리 작업 수행 가능 | 즉시 강제 종료 |
> | 사용 시점 | 일반적인 종료 | SIGTERM으로 안 될 때 |
>
> 항상 SIGTERM을 먼저 시도하고, 응답이 없을 때만 SIGKILL 사용.

---

## Question 10 - standalone vs inetd 적용 [analysis]
> 웹 서버(httpd)와 finger 서비스에 각각 어떤 데몬 실행 방식이 적합한지 근거와 함께 설명하시오.

> [!answer]- 정답 보기
> - **httpd → standalone**: 웹 서버는 요청이 빈번하므로 항상 메모리 상주하여 빠른 응답 필요
> - **finger → inetd**: 거의 사용되지 않는 서비스이므로 요청 시에만 실행하여 리소스 절약
> - 판단 기준: 요청 빈도와 응답 속도 요구사항

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | kill 기본 | SIGTERM (15) |
> | 강제 종료 | SIGKILL (9) |
> | 우선순위 최고 | NI = -20 |
> | 메모리 상주 | standalone |
> | 로그아웃 후 실행 | nohup |
> | crontab 순서 | 분 시 일 월 요일 |
