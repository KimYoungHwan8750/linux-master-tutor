---
source_pdf: programjy.tistory.com
part: "리눅스마스터 2급 2차 - X-Windows Practice"
keywords: practice, x-windows, desktop-environment, display-manager
---

# X-Windows Practice (9문제)

#practice #x-windows

## 관련 개념
- [[X-Windows]]
- [[장치 설정]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | X-Windows 구조 | 클라이언트/서버 |
> | Xlib 대체 (스레드 향상) | XCB |
> | Xorg 설정 파일 | xorg.conf |
> | 그래픽 부팅 (systemd) | graphical.target |
> | 텍스트 부팅 (systemd) | multi-user.target |
> | KDE 툴킷/윈도우매니저 | Qt / Kwin |
> | GNOME 툴킷/윈도우매니저 | GTK+ / Mutter |
> | GNOME DM | GDM |
> | KDE Plasma DM | SDDM |
> | 모든 호스트 허용 | xhost + |
> | 쿠키 기반 인증 | xauth |

---

## 문제 1 - X-Windows 기본 개념 [recall]
> X-Windows의 기본 구조를 설명하고, X서버와 X클라이언트의 역할 차이를 서술하시오.

> [!answer]- 정답 보기
> X-Windows는 **클라이언트/서버 구조**의 네트워크 기반 그래픽 환경이다.
>
> | 구성 | 역할 |
> |------|------|
> | **X서버** | 화면에 그래픽을 **표시**하는 프로그램 (사용자 앞의 디스플레이) |
> | **X클라이언트** | 그래픽 작업을 **요청**하는 프로그램 (원격에서 실행 가능) |
>
> 일반적인 네트워크와 **반대 구조**: 사용자가 보는 화면이 서버, 원격 프로그램이 클라이언트이다.

---

## 문제 2 - X프로토콜 메시지 [recall]
> X프로토콜에서 사용하는 4가지 메시지 타입을 적고, 각각의 전달 방향(클라이언트↔서버)을 서술하시오.

> [!answer]- 정답 보기
> | 메시지 | 방향 | 설명 |
> |--------|------|------|
> | **Request** (요청) | 클라이언트 → 서버 | 작업 요청 |
> | **Reply** (응답) | 서버 → 클라이언트 | 요청에 대한 결과 |
> | **Error** (오류) | 서버 → 클라이언트 | 오류 발생 알림 |
> | **Event** (이벤트) | 서버 → 클라이언트 | 마우스, 키보드 등 이벤트 전달 |
>
> **Request만** 클라이언트→서버 방향, 나머지 3개는 서버→클라이언트 방향이다.

---

## 문제 3 - 부팅 모드 [recall]
> 다음 빈칸을 채우시오.
> - X-Windows(그래픽) 부팅: systemd에서는 `(가)`, SysV에서는 runlevel `(나)`
> - 텍스트(CLI) 부팅: systemd에서는 `(다)`, SysV에서는 runlevel `(라)`
> - 기본 부팅 모드 변경 명령어: `(마)`

> [!answer]- 정답 보기
> - **(가)**: `graphical.target`
> - **(나)**: `5`
> - **(다)**: `multi-user.target`
> - **(라)**: `3`
> - **(마)**: `systemctl set-default`
>
> ```bash
> # 그래픽 모드로 기본 설정
> systemctl set-default graphical.target
> # 텍스트 모드로 기본 설정
> systemctl set-default multi-user.target
> # 현재 기본 모드 확인
> systemctl get-default
> ```

---

## 문제 4 - 데스크톱 환경 비교 [recall]
> 다음 표의 빈칸을 채우시오.
> | 환경 | 툴킷 | 윈도우 매니저 |
> |------|-------|-------------|
> | KDE | (가) | (나) |
> | GNOME | (다) | (라) |
> | XFCE | (마) | (바) |
> | LXDE | (사) | (아) |

> [!answer]- 정답 보기
> | 환경 | 툴킷 | 윈도우 매니저 |
> |------|-------|-------------|
> | KDE | **(가) Qt** | **(나) Kwin** |
> | GNOME | **(다) GTK+** | **(라) Metacity/Mutter** |
> | XFCE | **(마) GTK+** | **(바) Xfwm** |
> | LXDE | **(사) GTK+** | **(아) Openbox** |
>
> KDE만 Qt, 나머지는 모두 GTK+ 사용

---

## 문제 5 - 디스플레이 매니저 [recall]
> 다음 설명에 해당하는 디스플레이 매니저를 적으시오.
> (1) GNOME 기본 디스플레이 매니저
> (2) KDE Plasma 5에서 KDM을 대체한 디스플레이 매니저
> (3) 경량 범용 디스플레이 매니저

> [!answer]- 정답 보기
> | 번호 | 디스플레이 매니저 | 설명 |
> |------|------------------|------|
> | (1) | **GDM** (GNOME Display Manager) | GNOME 기본 |
> | (2) | **SDDM** (Simple Desktop Display Manager) | KDE Plasma 5+ 기본 |
> | (3) | **LightDM** (Light Display Manager) | 경량, 다양한 DE 지원 |

---

## 문제 6 - xhost 명령어 [application]
> 관리자가 IP 주소 `192.168.1.50`의 컴퓨터에서 X-Windows 프로그램을 현재 서버 화면에 표시하려 한다. xhost를 사용하여 해당 호스트를 허용하는 명령어와, 이후 접근을 다시 차단하는 명령어를 작성하시오.

> [!answer]- 정답 보기
> ```bash
> # 특정 호스트 허용
> xhost +192.168.1.50
>
> # 특정 호스트 차단
> xhost -192.168.1.50
> ```
>
> | 명령어 | 설명 |
> |--------|------|
> | `xhost +` | **모든** 호스트 허용 (보안 취약) |
> | `xhost -` | 접근 제한 활성화 |
> | `xhost +IP` | **특정** 호스트 허용 |
> | `xhost -IP` | **특정** 호스트 차단 |

---

## 문제 7 - xhost vs xauth [analysis]
> xhost와 xauth의 인증 방식, 보안 수준, 인증 단위를 비교하시오. 또한 xauth에서 쿠키값을 확인하는 명령어를 적으시오.

> [!answer]- 정답 보기
> | 구분 | xhost | xauth |
> |------|-------|-------|
> | 인증 방식 | **호스트(IP) 기반** | **쿠키(MIT-MAGIC-COOKIE) 기반** |
> | 보안 수준 | 낮음 | **높음** |
> | 인증 단위 | 호스트(컴퓨터) 단위 | 사용자(세션) 단위 |
>
> xauth 쿠키값 확인: **`xauth list`**
>
> xauth는 128비트 쿠키값을 `~/.Xauthority` 파일에 저장하여 인증한다.

---

## 문제 8 - DISPLAY 환경변수 [application]
> 원격 서버(IP: `10.0.0.5`)의 X클라이언트 프로그램을 로컬 X서버의 디스플레이 0, 스크린 0에 표시하려 한다. DISPLAY 환경변수를 설정하는 명령어를 작성하시오.

> [!answer]- 정답 보기
> ```bash
> export DISPLAY=10.0.0.5:0.0
> ```
>
> **DISPLAY 형식**: `IP주소:디스플레이번호.스크린번호`
> - IP주소: X서버의 주소 (여기서는 `10.0.0.5`)
> - 디스플레이 번호: 0 (기본)
> - 스크린 번호: 0 (기본)
>
> 주의: 이 명령은 **X클라이언트 측**에서 실행하여, 출력을 보낼 X서버를 지정한다.

---

## 문제 9 - 종합 분석 [analysis]
> Xorg 서버를 사용하는 리눅스 시스템에서 GNOME 데스크톱 환경을 기본 부팅 모드로 설정하려고 한다. 다음을 순서대로 답하시오.
> (1) Xorg의 설정 파일 경로
> (2) GNOME이 사용하는 툴킷과 윈도우 매니저
> (3) GNOME의 디스플레이 매니저
> (4) 그래픽 모드로 기본 부팅을 설정하는 명령어

> [!answer]- 정답 보기
> | 항목 | 답 |
> |------|-----|
> | (1) Xorg 설정 파일 | `/etc/X11/xorg.conf` (또는 `xorg.conf`) |
> | (2) GNOME 툴킷 | **GTK+** |
> | (2) GNOME 윈도우 매니저 | **Mutter** (GNOME 3) / Metacity (GNOME 2) |
> | (3) GNOME DM | **GDM** (GNOME Display Manager) |
> | (4) 그래픽 부팅 설정 | `systemctl set-default graphical.target` |

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | X-Windows 구조 | 클라이언트/서버 |
> | X프로토콜 4 메시지 | Request, Reply, Error, Event |
> | Xlib 기반 언어 | C/Lisp |
> | Xlib 대체 라이브러리 | XCB (스레드 향상) |
> | XFree86 설정 파일 | XF86Config |
> | Xorg 설정 파일 | xorg.conf |
> | 그래픽 모드 (systemd) | graphical.target (runlevel 5) |
> | 텍스트 모드 (systemd) | multi-user.target (runlevel 3) |
> | 부팅 모드 변경 | systemctl set-default |
> | KDE: 툴킷/WM/DM | Qt / Kwin / SDDM |
> | GNOME: 툴킷/WM/DM | GTK+ / Mutter / GDM |
> | XFCE 윈도우 매니저 | Xfwm |
> | LXDE 윈도우 매니저 | Openbox |
> | 저사양 경량 DE | LXDE |
> | 모든 호스트 허용 | xhost + |
> | 쿠키 인증 | xauth (MIT-MAGIC-COOKIE) |
> | DISPLAY 형식 | IP:디스플레이.스크린 |
