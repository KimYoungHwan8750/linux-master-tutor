---
source_pdf: programjy.tistory.com
part: "Part2 Ch03"
keywords: practice, process, signal, daemon, cron
---

# 프로세스관리 Practice (10문제)

#practice #process

## 관련 개념
- [[프로세스 관리]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | 모든 프로세스 풀 포맷 | ps -ef |
> | 강제 종료 시그널 | SIGKILL (9) |
> | kill 기본 시그널 | SIGTERM (15) |
> | Ctrl+C / Ctrl+Z | SIGINT(2) / SIGTSTP(20) |
> | nice 범위 | -20 ~ 19 |
> | 로그아웃 후에도 실행 | nohup |
> | 반복 예약 vs 일회성 | cron vs at |
> | 메모리 상주 데몬 | standalone |

---

## 문제 1 - 시그널 번호 [recall]
> 다음 시그널과 번호를 올바르게 연결하시오.
>
> A. SIGHUP &nbsp;&nbsp; B. SIGINT &nbsp;&nbsp; C. SIGKILL &nbsp;&nbsp; D. SIGTERM &nbsp;&nbsp; E. SIGTSTP
>
> ① 2 &nbsp;&nbsp; ② 9 &nbsp;&nbsp; ③ 15 &nbsp;&nbsp; ④ 20 &nbsp;&nbsp; ⑤ 1

> [!answer]- 정답 보기
> | 시그널 | 번호 | 의미 |
> |--------|------|------|
> | A. SIGHUP | **⑤ 1** | 재시작 (Hangup) |
> | B. SIGINT | **① 2** | 인터럽트, Ctrl+C |
> | C. SIGKILL | **② 9** | 강제 종료 (무시 불가) |
> | D. SIGTERM | **③ 15** | 정상 종료 (kill 기본값) |
> | E. SIGTSTP | **④ 20** | 일시 정지, Ctrl+Z |

---

## 문제 2 - ps 명령어 옵션 [recall]
> 시스템의 **모든 프로세스**를 **풀 포맷**으로 출력하는 명령어를 System V 스타일과 BSD 스타일로 각각 작성하시오.

> [!answer]- 정답 보기
> ```bash
> # System V 스타일
> ps -ef
>
> # BSD 스타일
> ps aux
> ```
> - `-e`: 모든 프로세스 (every)
> - `-f`: 풀 포맷 (full) - UID, PID, PPID 등 표시
> - `a`: 모든 사용자 프로세스
> - `u`: 사용자 중심 포맷 (%CPU, %MEM 등)
> - `x`: 터미널 없는 프로세스도 포함

---

## 문제 3 - 데몬 방식 구분 [recall]
> 다음 설명에 해당하는 데몬 실행 방식은?
>
> "**메모리에 항상 상주**하며 클라이언트 요청에 **즉시 응답**한다. httpd, sshd 같은 자주 사용하는 서비스에 적합하다."

> [!answer]- 정답 보기
> **standalone 방식**
> - 메모리에 상주하므로 즉시 응답 가능 (빠름)
> - 메모리 사용량은 많음
> - 반대: **inetd/xinetd 방식** = 요청 시 프로세스 생성, 메모리 효율적

---

## 문제 4 - nice 값 이해 [application]
> 다음 중 nice 값에 대한 설명으로 **옳은 것**을 모두 고르시오.
>
> ① nice 값의 범위는 -20 ~ 19이다
> ② nice 값이 높을수록 우선순위가 높다
> ③ 일반 사용자는 nice 값을 음수로 설정할 수 없다
> ④ renice는 프로세스 시작 시 우선순위를 지정한다
> ⑤ nice 기본값은 0이다

> [!answer]- 정답 보기
> **①, ③, ⑤**
>
> - ① 맞음: nice 값 범위는 **-20 ~ 19**
> - ② 틀림: nice 값이 **낮을수록** 우선순위가 높음 (-20이 가장 높음)
> - ③ 맞음: 일반 사용자는 **양수값만** 설정 가능 (우선순위 낮추기만)
> - ④ 틀림: renice는 **실행 중** 프로세스의 우선순위 변경 (시작 시는 nice)
> - ⑤ 맞음: nice 기본값은 **0**

---

## 문제 5 - crontab 해석 [application]
> 다음 crontab 항목이 실행되는 시간을 설명하시오.
>
> ```
> 30 2 1,15 * * /home/june/backup.sh
> ```

> [!answer]- 정답 보기
> **매월 1일과 15일 오전 2시 30분**에 /home/june/backup.sh를 실행한다.
>
> | 필드 | 값 | 의미 |
> |------|-----|------|
> | 분 | 30 | 30분 |
> | 시 | 2 | 오전 2시 |
> | 일 | 1,15 | 1일과 15일 (,는 여러 값 나열) |
> | 월 | * | 매월 |
> | 요일 | * | 모든 요일 |

---

## 문제 6 - crontab 작성 [application]
> 다음 조건에 맞는 crontab 항목을 작성하시오.
>
> "**매주 월요일부터 금요일**, **오전 9시**에 `/home/june/work.sh`를 실행"

> [!answer]- 정답 보기
> ```
> 0 9 * * 1-5 /home/june/work.sh
> ```
> - 분: 0 (정각)
> - 시: 9 (오전 9시)
> - 일: * (매일)
> - 월: * (매월)
> - 요일: 1-5 (월~금, 0=일요일, 1=월요일, ..., 5=금요일)

---

## 문제 7 - nohup 명령어 [recall]
> 사용자가 로그아웃한 후에도 `backup.sh` 스크립트가 백그라운드에서 계속 실행되도록 하는 명령어를 작성하시오.

> [!answer]- 정답 보기
> ```bash
> nohup ./backup.sh &
> ```
> - **nohup**: SIGHUP(1번) 시그널을 무시하여 로그아웃 후에도 계속 실행
> - **&**: 백그라운드에서 실행
> - 출력은 기본적으로 **nohup.out** 파일에 저장됨
> - 출력을 지정하려면: `nohup ./backup.sh > output.log 2>&1 &`

---

## 문제 8 - kill 명령어 [application]
> PID가 5678인 프로세스를 **정상 종료**하는 명령어와 **강제 종료**하는 명령어를 각각 작성하시오.

> [!answer]- 정답 보기
> ```bash
> # 정상 종료 (SIGTERM, 15번)
> kill 5678
> # 또는
> kill -15 5678
>
> # 강제 종료 (SIGKILL, 9번)
> kill -9 5678
> ```
> - kill의 기본 시그널은 **SIGTERM(15)**이므로 번호 없이 `kill PID`만 쓰면 정상 종료
> - SIGKILL(9)은 무시/차단 불가능한 강제 종료

---

## 문제 9 - 작업 제어 순서 [analysis]
> 다음 상황에서 실행해야 할 명령어를 순서대로 나열하시오.
>
> "포그라운드에서 실행 중인 프로세스를 일시 정지하고, 백그라운드에서 재개한 후, 다시 포그라운드로 전환하시오."

> [!answer]- 정답 보기
> ```bash
> # 1. 포그라운드 프로세스 일시 정지
> Ctrl+Z                  # SIGTSTP(20) 시그널 전송
>
> # 2. 백그라운드에서 재개
> bg %1                   # 작업 번호 1을 백그라운드에서 계속 실행
>
> # 3. 다시 포그라운드로 전환
> fg %1                   # 작업 번호 1을 포그라운드로 전환
> ```
> - Ctrl+Z: SIGTSTP(20) → 일시 정지 (Stopped 상태)
> - bg: Stopped → Running (백그라운드)
> - fg: 백그라운드 → 포그라운드

---

## 문제 10 - 종합 분석 [analysis]
> 다음 상황을 분석하고 적절한 명령어를 제시하시오.
>
> 시스템 관리자가 서버의 httpd 프로세스가 많은 CPU를 사용하고 있음을 발견했다.
> 1. 실시간으로 프로세스 상태를 모니터링하는 명령어
> 2. httpd 프로세스의 PID를 확인하는 명령어
> 3. httpd 프로세스의 우선순위를 낮추는(nice 값 10) 명령어
> 4. 모든 httpd 프로세스를 정상 종료하는 명령어

> [!answer]- 정답 보기
> ```bash
> # 1. 실시간 모니터링
> top
>
> # 2. httpd PID 확인
> ps -ef | grep httpd
> # 또는
> pgrep httpd
>
> # 3. 실행 중인 httpd의 우선순위 변경 (PID가 1234라면)
> renice -n 10 1234
>
> # 4. 모든 httpd 정상 종료
> killall httpd
> # 또는
> killall -15 httpd
> ```
> - **top**: 실시간 모니터링
> - **ps -ef | grep**: 특정 프로세스 PID 확인
> - **renice**: 실행 중 프로세스의 nice 값 변경 (nice는 시작 시)
> - **killall**: 프로세스 이름으로 종료 (kill은 PID 필요)

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | SIGHUP/SIGINT/SIGKILL/SIGTERM/SIGTSTP | 1/2/9/15/20 |
> | 모든 프로세스 풀 포맷 | ps -ef 또는 ps aux |
> | 메모리 상주 데몬 | standalone |
> | nice 범위, 낮을수록 | -20~19, 높은 우선순위 |
> | 매월 1,15일 2시 30분 | 30 2 1,15 * * |
> | 월~금 오전 9시 | 0 9 * * 1-5 |
> | 로그아웃 후에도 실행 | nohup 명령어 & |
> | 정상/강제 종료 | kill(기본15) / kill -9 |
> | Ctrl+Z → bg → fg | 일시정지 → 백그라운드 → 포그라운드 |
> | 이름으로 종료 | killall |
