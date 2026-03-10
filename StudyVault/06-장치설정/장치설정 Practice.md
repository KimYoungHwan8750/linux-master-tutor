---
source_pdf: programjy.tistory.com
part: "리눅스마스터 2급 2차 - 장치설정 Practice"
keywords: practice, printer, sound, scanner
---

# 장치설정 Practice (9문제)

#practice #device

## 관련 개념
- [[장치 설정]]
- [[X-Windows]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | 애플 개발 인쇄 시스템 | CUPS |
> | CUPS 설정 파일 | `/etc/cups/cupsd.conf` |
> | CUPS 프로토콜 | HTTP, IPP, SMB |
> | CUPS 웹 포트 | 631 |
> | LPRng 설정 파일 | `/etc/printcap` |
> | BSD 출력 요청 | `lpr` |
> | System V 출력 요청 | `lp` |
> | 리눅스 사운드 표준 | ALSA |
> | SANE GUI 프론트엔드 | XSANE |

---

## 문제 1 - CUPS 기본 [recall]
> 리눅스 시스템의 표준 인쇄 시스템으로, 애플이 개발하였으며 HTTP, IPP, SMB 프로토콜을 사용하는 인쇄 시스템의 이름은?

> [!answer]- 정답 보기
> **CUPS** (Common Unix Printing System)
>
> - 애플(Apple)에서 개발
> - HTTP, **IPP**(Internet Printing Protocol), SMB 프로토콜 사용
> - 웹 브라우저를 통해 관리 가능 (포트 **631**)
> - 설정 파일: `/etc/cups/cupsd.conf`

---

## 문제 2 - CUPS 설정 파일 [recall]
> CUPS의 주요 설정 파일 3가지와 각각의 역할을 서술하시오.

> [!answer]- 정답 보기
> | 설정 파일 | 역할 |
> |-----------|------|
> | `/etc/cups/cupsd.conf` | CUPS **데몬(서버)** 설정 (포트, 접근제어, 로그 등) |
> | `/etc/cups/printers.conf` | **프린터** 설정 정보 (장치, 드라이버 등) |
> | `/etc/cups/classes.conf` | 프린터 **클래스(그룹)** 설정 |

---

## 문제 3 - BSD vs System V 명령어 [recall]
> 다음 표의 빈칸을 채우시오.
> | 기능 | BSD 계열 | System V 계열 |
> |------|----------|---------------|
> | 출력 요청 | (가) | (나) |
> | 큐 확인 | (다) | (라) |
> | 작업 삭제 | (마) | (바) |

> [!answer]- 정답 보기
> | 기능 | BSD 계열 | System V 계열 |
> |------|----------|---------------|
> | 출력 요청 | **(가) lpr** | **(나) lp** |
> | 큐 확인 | **(다) lpq** | **(라) lpstat** |
> | 작업 삭제 | **(마) lprm** | **(바) cancel** |
>
> - BSD: lpr, lpq, lprm, lpc
> - System V: lp, lpstat, cancel

---

## 문제 4 - LPRng vs CUPS [application]
> 관리자가 웹 브라우저로 프린터를 관리하려 한다. `http://localhost:631`에 접속하면 프린터 관리 화면이 나타날 때, 이 인쇄 시스템은 무엇이고, LPRng와의 차이점 2가지를 서술하시오.

> [!answer]- 정답 보기
> 인쇄 시스템: **CUPS**
>
> | 차이점 | CUPS | LPRng |
> |--------|------|-------|
> | 웹 관리 | O (포트 631) | X |
> | 프로토콜 | HTTP, IPP, SMB | LPD |
> | 설정 파일 | `/etc/cups/cupsd.conf` | `/etc/printcap` |

---

## 문제 5 - 사운드 시스템 [recall]
> 리눅스 커널 요소로 포함되어 있으며, 사운드 카드의 자동 구성과 다중 장치 관리를 지원하는 사운드 시스템의 이름은?

> [!answer]- 정답 보기
> **ALSA** (Advanced Linux Sound Architecture)
>
> - 리눅스 **커널** 요소로 포함
> - 사운드 카드 **자동 구성** 지원
> - **다중 사운드 장치** 동시 관리 가능
> - OSS 호환 모듈 제공
> - OSS를 대체하는 현재 리눅스 표준

---

## 문제 6 - OSS vs ALSA [analysis]
> OSS와 ALSA를 대상 OS, 기반 기술, 현재 상태 측면에서 비교하시오.

> [!answer]- 정답 보기
> | 구분 | OSS | ALSA |
> |------|-----|------|
> | 대상 OS | 유닉스 전반 | **리눅스 전용** |
> | 기반 기술 | **POSIX** 시스템 호출 (read, write, ioctl) | **리눅스 커널 모듈** |
> | 자동 구성 | 미지원 | 지원 |
> | 다중 장치 | 제한적 | 지원 |
> | 현재 상태 | 레거시 (대체됨) | **리눅스 표준** |
>
> ALSA는 OSS를 대체하면서도 **OSS 호환 모듈**을 제공하여 기존 OSS 기반 프로그램도 동작 가능하다.

---

## 문제 7 - 사운드 명령어 [recall]
> 다음 설명에 해당하는 명령어를 적으시오.
> (1) ALSA 사운드 카드를 제어하는 명령어
> (2) 커서(ncurses) 기반 오디오 믹서 프로그램
> (3) CD에서 오디오 트랙을 추출(리핑)하는 명령어

> [!answer]- 정답 보기
> | 번호 | 명령어 | 설명 |
> |------|--------|------|
> | (1) | `alsactl` | ALSA 카드 제어 (설정 저장/복원) |
> | (2) | `alsamixer` | 터미널 기반 오디오 믹서 |
> | (3) | `cdparanoia` | CD → WAV 오디오 추출 |

---

## 문제 8 - SANE/XSANE [recall]
> 스캐너를 관리하기 위한 API인 SANE과 XSANE의 관계를 설명하고, 스캐너 관련 명령어 4가지를 나열하시오.

> [!answer]- 정답 보기
> **관계**: SANE은 이미지 하드웨어를 제어하는 **API(백엔드)**, XSANE은 SANE의 **X-Windows 기반 GUI 프론트엔드**
>
> | 명령어 | 기능 |
> |--------|------|
> | `sane-find-scanner` | 스캐너 **장치 검색** |
> | `scanimage` | CLI에서 **이미지 스캔** |
> | `scanadf` | **ADF**(자동 문서 급지) 다중 스캔 |
> | `xcam` | **GUI** 기반 스캔 프로그램 |

---

## 문제 9 - 종합 분석 [analysis]
> 리눅스에서 프린터, 사운드, 스캐너의 "현대적 표준 시스템"을 각각 하나씩 적고, 공통적인 발전 방향(레거시 → 현대)의 특징을 2가지 서술하시오.

> [!answer]- 정답 보기
> | 장치 | 레거시 | 현대적 표준 |
> |------|--------|-------------|
> | 프린터 | LPRng | **CUPS** |
> | 사운드 | OSS | **ALSA** |
> | 스캐너 | (직접 접근) | **SANE/XSANE** |
>
> **공통적인 발전 방향**:
> 1. **자동 구성/감지**: 수동 설정 → 자동화 (ALSA의 자동 구성, CUPS의 자동 장치 감지)
> 2. **웹/GUI 관리 지원**: 명령줄 전용 → 웹/그래픽 인터페이스 (CUPS의 웹 관리, XSANE의 GUI)
>
> 추가: 다중 장치 지원, 표준 프로토콜 채택, 커널/시스템 통합 강화

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | 애플 인쇄 시스템 | CUPS |
> | CUPS 설정 파일 | `/etc/cups/cupsd.conf` |
> | CUPS 포트 | 631 |
> | CUPS 프로토콜 | HTTP, IPP, SMB |
> | LPRng 설정 파일 | `/etc/printcap` |
> | BSD 출력/큐/삭제 | lpr / lpq / lprm |
> | SysV 출력/큐/취소 | lp / lpstat / cancel |
> | 리눅스 사운드 표준 | ALSA (커널 요소) |
> | POSIX 사운드 | OSS |
> | ALSA 믹서 | alsamixer |
> | CD 추출 | cdparanoia |
> | 스캐너 API | SANE |
> | SANE GUI | XSANE |
> | 스캐너 검색 | sane-find-scanner |
> | ADF 다중 스캔 | scanadf |
