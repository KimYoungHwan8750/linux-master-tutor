---
source_pdf: 원문 미보유 (웹 소스)
part: Part 2 Ch06
keywords: practice, printer, sound, scanner, cups
---

# 장치설정 Practice (8 questions)

#practice #device

## Related Concepts
- [[장치 설정]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | 프린터 표준 | CUPS |
> | CUPS 포트 | 631 |
> | 사운드 표준 | ALSA |
> | 스캐너 백엔드 | SANE |
> | 인쇄 큐 확인 | lpq |

---

## Question 1 - CUPS 기본 [recall]
> 리눅스에서 현재 표준으로 사용되는 프린터 관리 시스템은?

> [!answer]- 정답 보기
> **CUPS** (Common Unix Printing System) — 웹 기반 관리, IPP 프로토콜 사용

---

## Question 2 - CUPS 포트 [recall]
> CUPS의 웹 관리 인터페이스에 접속하기 위한 포트 번호는?

> [!answer]- 정답 보기
> **631** — `http://localhost:631`로 접속

---

## Question 3 - 프린터 명령어 [recall]
> 인쇄 대기열에 있는 작업을 확인하는 BSD 계열 명령은?

> [!answer]- 정답 보기
> **lpq** — 인쇄 큐(queue)를 확인. System V 계열은 `lpstat`

---

## Question 4 - 사운드 시스템 [recall]
> 리눅스에서 현재 표준 사운드 시스템은?

> [!answer]- 정답 보기
> **ALSA** (Advanced Linux Sound Architecture) — OSS를 대체

---

## Question 5 - 스캐너 구조 [recall]
> SANE과 XSANE의 관계를 설명하시오.

> [!answer]- 정답 보기
> **SANE** = 백엔드 (스캐너 드라이버/하드웨어 접근), **XSANE** = 프론트엔드 (GUI). XSANE이 SANE을 이용하여 스캔 수행.

---

## Question 6 - 인쇄 작업 관리 [application]
> 인쇄 큐에 잘못 보낸 작업을 취소하려면 어떤 명령을 사용하는가? BSD와 System V 방식 모두 답하시오.

> [!answer]- 정답 보기
> - BSD: **lprm** (작업 번호 지정)
> - System V: **cancel** (작업 번호 지정)
> 먼저 `lpq`(또는 `lpstat`)로 작업 번호 확인 후 취소

---

## Question 7 - CUPS 설정 [application]
> CUPS의 설정 파일 경로와 CUPS에서 사용하는 프로토콜은?

> [!answer]- 정답 보기
> - 설정 파일: `/etc/cups/cupsd.conf`
> - 프로토콜: **IPP** (Internet Printing Protocol)

---

## Question 8 - BSD vs System V 비교 [analysis]
> 프린터 관련 BSD 계열 명령어와 System V 계열 명령어를 비교하시오.

> [!answer]- 정답 보기
> | 기능 | BSD 계열 | System V 계열 |
> |------|---------|---------------|
> | 인쇄 | lpr | lp |
> | 큐 확인 | lpq | lpstat |
> | 취소 | lprm | cancel |
> | 제어 | lpc | — |
>
> 두 계열 모두 알아야 시험에서 혼동하지 않음

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | 프린터 표준 | CUPS (포트 631) |
> | 사운드 표준 | ALSA |
> | 스캐너 백엔드 | SANE |
> | BSD 인쇄 | lpr |
> | BSD 큐 확인 | lpq |
> | BSD 취소 | lprm |
