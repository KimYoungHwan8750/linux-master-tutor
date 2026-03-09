---
source_pdf: 원문 미보유 (웹 소스)
part: Part 3 Ch01
keywords: practice, x-windows, desktop, xhost, xauth
---

# X-Windows Practice (8 questions)

#practice #x-windows

## Related Concepts
- [[X-Windows]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | X-Windows 실행 | startx |
> | GUI 부팅 | graphical.target (runlevel 5) |
> | 보안 인증 | xauth |
> | KDE 툴킷 | Qt |
> | 경량 DE | XFCE, LXDE |

---

## Question 1 - X-Windows 구조 [recall]
> X-Windows에서 X서버와 X클라이언트의 역할을 각각 설명하시오.

> [!answer]- 정답 보기
> - **X서버**: 디스플레이 장치에서 화면 출력과 키보드/마우스 입력 처리 (사용자 측)
> - **X클라이언트**: 응용 프로그램 실행 (원격에서도 실행 가능)
> 일반적인 서버-클라이언트 개념과 **반대**임에 주의

---

## Question 2 - 부팅 모드 [recall]
> 리눅스를 GUI 모드로 부팅하기 위한 systemd target은?

> [!answer]- 정답 보기
> **graphical.target** (runlevel 5). CLI 부팅은 multi-user.target (runlevel 3).
> `systemctl set-default graphical.target`으로 설정

---

## Question 3 - 데스크톱 환경 [recall]
> Qt 툴킷을 사용하는 데스크톱 환경은?

> [!answer]- 정답 보기
> **KDE** — 나머지 GNOME, XFCE, LXDE는 모두 GTK 사용

---

## Question 4 - X 인증 [recall]
> xhost와 xauth 중 보안이 더 강한 방식과 그 이유는?

> [!answer]- 정답 보기
> **xauth** — MIT-MAGIC-COOKIE **토큰 기반** 인증으로, IP만으로 허용하는 xhost보다 보안이 강함

---

## Question 5 - startx [recall]
> CLI 모드(multi-user.target)에서 X-Windows를 시작하는 명령은?

> [!answer]- 정답 보기
> **startx** — xinit을 호출하여 X서버와 세션을 시작

---

## Question 6 - 윈도우 매니저 [recall]
> KDE와 GNOME의 기본 윈도우 매니저는 각각 무엇인가?

> [!answer]- 정답 보기
> - KDE: **Kwin**
> - GNOME: **Mutter**

---

## Question 7 - 원격 X 설정 [application]
> 원격 서버(192.168.1.50)의 X클라이언트 출력을 로컬에서 보려면 어떤 설정이 필요한가?

> [!answer]- 정답 보기
> 1. 로컬(X서버)에서: `xhost +192.168.1.50` (접근 허용)
> 2. 원격(X클라이언트)에서: `export DISPLAY=로컬IP:0.0` (출력 대상 지정)
> 보안을 위해서는 xhost 대신 `xauth` + SSH X11 forwarding 사용 권장

---

## Question 8 - DE 선택 기준 [analysis]
> 구형 저사양 시스템에 적합한 데스크톱 환경을 추천하고, KDE/GNOME과 비교하여 근거를 제시하시오.

> [!answer]- 정답 보기
> **LXDE** 또는 **XFCE** 추천
> | DE | 리소스 사용 | 기능 | 적합 환경 |
> |----|-----------|------|-----------|
> | KDE | 높음 | 풍부 | 고사양 |
> | GNOME | 중간 | 중간 | 중사양 |
> | XFCE | 낮음 | 적당 | 저사양 |
> | LXDE | 최저 | 기본 | 최저사양 |
>
> 저사양에서는 메모리와 CPU 사용이 적은 LXDE가 가장 적합

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | X-Windows 실행 | startx |
> | GUI 부팅 | graphical.target |
> | CLI 부팅 | multi-user.target |
> | 보안 인증 | xauth |
> | KDE 툴킷 | Qt |
> | 경량 DE | LXDE |
