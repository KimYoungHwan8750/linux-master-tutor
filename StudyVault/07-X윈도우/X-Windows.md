---
source_pdf: programjy.tistory.com
part: "리눅스마스터 2급 2차 - X-Windows"
keywords: x-windows, desktop-environment, display-manager, window-manager, xhost
---

# X-Windows (★★★)

#linux-master #x-windows #desktop-env #display-mgr #window-mgr

## 한눈에 비교

### X-Windows 아키텍처 계층도

```
┌──────────────────────────────────────────────────────┐
│  사용자                                               │
│  ┌────────────────────────────────────────────────┐   │
│  │  데스크톱 환경 (KDE, GNOME, XFCE, LXDE)        │   │
│  │  ┌──────────────────────────────────────────┐   │   │
│  │  │  윈도우 매니저 (Kwin, Mutter, Xfwm 등)   │   │   │
│  │  └──────────────────────────────────────────┘   │   │
│  └────────────────────────────────────────────────┘   │
│  ┌────────────────────────────────────────────────┐   │
│  │  디스플레이 매니저 (GDM, KDM, SDDM, LightDM)  │   │
│  └────────────────────────────────────────────────┘   │
│  ┌────────────────────────────────────────────────┐   │
│  │  X서버 (Xorg / XFree86)                        │   │
│  │  ┌───────────┐  ┌───────────┐  ┌───────────┐   │   │
│  │  │ Xlib/XCB  │  │ Xtoolkit  │  │ X프로토콜  │   │   │
│  │  └───────────┘  └───────────┘  └───────────┘   │   │
│  └────────────────────────────────────────────────┘   │
│  하드웨어 (그래픽 카드, 모니터, 키보드, 마우스)       │
└──────────────────────────────────────────────────────┘
```

---

## 1. X-Windows 개념

### 1-1. 기본 개념

- **네트워크 기반** 그래픽 환경 시스템
- **이기종(異機種) 시스템** 간 호환 가능
- **클라이언트/서버 구조** 사용
  - **X서버**: 화면에 그래픽을 표시하는 프로그램 (사용자 앞의 컴퓨터)
  - **X클라이언트**: 그래픽 작업을 요청하는 프로그램 (원격 가능)
- MIT에서 개발, 1984년 시작
- 현재 버전: X11 (X Window System version 11)

> [!warning] X-Windows 클라이언트/서버 주의
> 일반적인 네트워크와 **반대 구조**:
> - **X서버** = 사용자가 보는 화면 (디스플레이 담당)
> - **X클라이언트** = 프로그램 (원격 서버에서 실행될 수 있음)

### 1-2. X프로토콜

X클라이언트와 X서버 사이의 통신 규약으로, 4가지 메시지 타입이 있다.

| 메시지 | 방향 | 설명 |
|--------|------|------|
| **Request** (요청) | 클라이언트 → 서버 | 클라이언트가 서버에 작업 요청 |
| **Reply** (응답) | 서버 → 클라이언트 | 서버가 요청에 대한 결과 응답 |
| **Error** (오류) | 서버 → 클라이언트 | 요청 처리 중 오류 발생 알림 |
| **Event** (이벤트) | 서버 → 클라이언트 | 마우스 클릭, 키 입력 등 이벤트 전달 |

### 1-3. 핵심 라이브러리

| 라이브러리 | 설명 | 특징 |
|------------|------|------|
| **Xlib** | X 클라이언트 라이브러리 | **C/Lisp** 언어 기반, 가장 기본 |
| **XCB** (X protocol C-language Binding) | Xlib 대체 라이브러리 | **스레드(Thread) 성능** 향상, 경량화 |
| **Xtoolkit** (Xt) | 고급 GUI 위젯 라이브러리 | Xlib 위에 구축, **위젯** 기반 개발 |

### 1-4. X서버 구현

#### XFree86

- **인텔 X86** 계열 하드웨어용 X서버
- 설정 파일: **`XF86Config`** 또는 `/etc/X11/XF86Config`
- 과거에 가장 많이 사용됨
- 라이선스 변경으로 인해 Xorg로 대체

#### Xorg

- **현대적** X 디스플레이 서버
- XFree86에서 포크(fork)하여 개발
- 설정 파일: **`xorg.conf`** 또는 `/etc/X11/xorg.conf`
- 현재 리눅스 표준 X서버
- 자동 하드웨어 감지 기능 제공

| 구분 | XFree86 | Xorg |
|------|---------|------|
| 대상 | 인텔 X86 | 범용 |
| 설정 파일 | `XF86Config` | `xorg.conf` |
| 현재 상태 | 레거시 | **현대적 표준** |

#### xorg.conf 주요 섹션

| 섹션 | 설명 |
|------|------|
| `ServerLayout` | 전체 레이아웃 설정 |
| `Files` | 폰트/모듈 경로 |
| `Module` | 로드할 모듈 |
| `InputDevice` | 키보드, 마우스 설정 |
| `Monitor` | 모니터 설정 |
| `Device` | 그래픽 카드 설정 |
| `Screen` | 해상도, 색 깊이 |

---

## 2. 부팅 모드

### systemd vs SysV 런레벨

| 모드 | systemd (target) | SysV (runlevel) | 설명 |
|------|-------------------|-----------------|------|
| 종료 | `poweroff.target` | runlevel 0 | 시스템 종료 |
| 단일 사용자 | `rescue.target` | runlevel 1 | 복구 모드 |
| 다중 사용자 (NFS 없음) | `multi-user.target` | runlevel 2 | — |
| **텍스트 (CLI)** | **`multi-user.target`** | **runlevel 3** | 네트워크 O, X윈도우 X |
| 미사용 | — | runlevel 4 | 사용자 정의 |
| **그래픽 (X윈도우)** | **`graphical.target`** | **runlevel 5** | 네트워크 O, X윈도우 O |
| 재부팅 | `reboot.target` | runlevel 6 | 시스템 재시작 |

> [!important] 시험 핵심
> - 텍스트 모드: `multi-user.target` = runlevel **3**
> - 그래픽 모드: `graphical.target` = runlevel **5**

### 부팅 모드 변경 명령어

```bash
# 현재 기본 부팅 모드 확인
systemctl get-default

# 그래픽 모드로 기본 변경
systemctl set-default graphical.target

# 텍스트 모드로 기본 변경
systemctl set-default multi-user.target

# 즉시 모드 전환 (재부팅 없이)
systemctl isolate graphical.target
systemctl isolate multi-user.target

# SysV 방식 (레거시)
init 3   # 텍스트 모드
init 5   # 그래픽 모드
```

---

## 3. 윈도우 매니저 (Window Manager)

> [!info] 윈도우 매니저는 창의 **배치, 크기 조절, 이동, 최소화/최대화** 등 **창의 표현**을 담당하는 프로그램이다.

### 주요 윈도우 매니저

| 윈도우 매니저 | 연관 환경 | 특징 |
|--------------|-----------|------|
| **Metacity** | GNOME 2 | GNOME 2 기본 윈도우 매니저 |
| **Mutter** | GNOME 3 | GNOME 3 기본 (Metacity 후속) |
| **Kwin** | KDE | KDE 기본 윈도우 매니저 |
| **Xfwm** | XFCE | XFCE 기본 윈도우 매니저 |
| **Openbox** | LXDE | LXDE 기본 윈도우 매니저 |
| **fvwm** | 독립 | 경량, 가상 데스크톱 지원 |
| **twm** | 독립 | Tab Window Manager, X11 기본 |
| **mwm** | 독립 | Motif Window Manager |
| **WindowMaker** | 독립 | NeXTSTEP 스타일 |
| **AfterStep** | 독립 | NeXTSTEP 스타일 변형 |

---

## 4. 데스크톱 환경 (Desktop Environment)

> [!info] 데스크톱 환경은 윈도우 매니저 + 파일 관리자 + 패널 + 설정 도구 등을 통합한 **완전한 그래픽 사용 환경**이다.

### 주요 데스크톱 환경 비교표

| 환경 | 툴킷 | 윈도우 매니저 | 특징 |
|------|-------|-------------|------|
| **KDE** | **Qt** (노키아→현재 Qt Company) | **Kwin** | 풍부한 기능, 높은 커스터마이즈 |
| **GNOME** | **GTK+** (GNU 프로젝트) | **Metacity/Mutter** | 오픈소스, 심플한 디자인 |
| **LXDE** | **GTK+** | **Openbox** | **저사양** 경량 데스크톱 |
| **XFCE** | **GTK+** | **Xfwm** | **경량** 윈도우 매니저, 속도 중시 |

> [!tip] 툴킷 구분 기억법
> - **KDE** = **Qt** (K와 Q 모두 특이한 글자)
> - **나머지** (GNOME, LXDE, XFCE) = **GTK+** (GNU 프로젝트)

### 추가 데스크톱 환경

| 환경 | 특징 |
|------|------|
| **Cinnamon** | GNOME 3 포크, Linux Mint 기본 |
| **MATE** | GNOME 2 포크, 전통적 인터페이스 |
| **Unity** | 우분투 전용 (현재 미사용) |
| **Budgie** | Solus 프로젝트, 현대적 |

---

## 5. 디스플레이 매니저 (Display Manager)

> [!info] 디스플레이 매니저는 **로그인 화면**을 관리하고, 사용자 인증 후 데스크톱 세션을 시작하는 프로그램이다.

### 주요 디스플레이 매니저

| 디스플레이 매니저 | 풀네임 | 연관 환경 | 특징 |
|------------------|--------|-----------|------|
| **XDM** | X Display Manager | X11 기본 | 가장 기본적인 DM |
| **GDM** | GNOME Display Manager | **GNOME** | GNOME 기본 DM |
| **KDM** | KDE Display Manager | **KDE** (4 이하) | KDE 4 기본 DM |
| **SDDM** | Simple Desktop Display Manager | **KDE Plasma** (5+) | KDM 후속, Qt 기반 |
| **LightDM** | Light Display Manager | **경량** (다목적) | 경량, 다양한 DE 지원 |
| **LXDM** | LXDE Display Manager | **LXDE** | LXDE 전용 |

> [!tip] 디스플레이 매니저 연관 기억
> - **G**DM → **G**NOME
> - **K**DM → **K**DE (구버전)
> - **S**DDM → KDE Plasma (신버전, **S**imple)
> - **LX**DM → **LX**DE
> - **Light**DM → 가벼운(Light) 범용

---

## 6. 원격 접근 제어

### 6-1. xhost (호스트 기반 인증)

> [!info] xhost는 **호스트(IP) 기반**으로 X서버에 대한 접근을 제어하는 명령어이다.

| 명령어 | 설명 |
|--------|------|
| `xhost` | 현재 접근 제어 상태 확인 |
| `xhost +` | **모든 클라이언트 허용** (보안 취약) |
| `xhost -` | **접근 제한** (허용 목록만 접근 가능) |
| `xhost +IP주소` | **특정 호스트 허용** |
| `xhost -IP주소` | **특정 호스트 차단** |
| `xhost +hostname` | 호스트명으로 허용 |

```bash
# 예시
xhost +                        # 모든 호스트 허용
xhost -                        # 접근 제한 활성화
xhost +192.168.1.100           # 특정 IP 허용
xhost -192.168.1.100           # 특정 IP 차단
xhost +local:                  # 로컬 접속 허용
```

> [!warning] `xhost +`는 보안에 매우 취약하므로 테스트 환경에서만 사용해야 한다.

### 6-2. xauth (MIT-MAGIC-COOKIE 기반 인증)

> [!info] xauth는 **쿠키(Cookie) 기반**으로 X서버 접근을 인증하는 보안 강화 방식이다.

- 인증 방식: **MIT-MAGIC-COOKIE-1** (128비트 쿠키값)
- 쿠키 파일: `~/.Xauthority`

| 명령어 | 설명 |
|--------|------|
| `xauth list` | 현재 **쿠키값** 확인 (display별) |
| `xauth add 디스플레이 . 쿠키값` | 쿠키 **추가** |
| `xauth remove 디스플레이` | 쿠키 **삭제** |
| `xauth generate 디스플레이 .` | 새 쿠키 **생성** |
| `xauth info` | xauth 정보 확인 |

```bash
# 예시
xauth list                     # 쿠키 목록 확인
xauth add :0 . abc123def456    # 쿠키 추가
xauth remove :0                # 쿠키 삭제
```

### xhost vs xauth 비교

| 구분 | xhost | xauth |
|------|-------|-------|
| 인증 방식 | **호스트(IP) 기반** | **쿠키(Cookie) 기반** |
| 인증 단위 | 호스트(컴퓨터) | 사용자(세션) |
| 보안 수준 | 낮음 | **높음** |
| 키워드 | IP 허용/차단 | MIT-MAGIC-COOKIE |
| 편의성 | 간편 | 복잡 |

### 6-3. DISPLAY 환경변수

X클라이언트가 어떤 X서버의 디스플레이에 출력할지를 지정하는 환경변수이다.

**형식**: `IP주소:디스플레이번호.스크린번호`

```bash
# 설정 예시
export DISPLAY=192.168.1.100:0.0
# IP: 192.168.1.100
# 디스플레이 번호: 0
# 스크린 번호: 0

# 로컬 디스플레이
export DISPLAY=:0
export DISPLAY=:0.0

# 원격 디스플레이
export DISPLAY=10.0.0.5:1.0

# 확인
echo $DISPLAY
```

---

## 시험 빈출 패턴

| 시나리오/키워드 | 정답 |
|----------------|------|
| X-Windows의 구조 | **클라이언트/서버** 구조 |
| X프로토콜 메시지 4가지 | Request, Reply, Error, Event |
| Xlib 대체, 스레드 향상 | **XCB** |
| XFree86 설정 파일 | `XF86Config` |
| Xorg 설정 파일 | `xorg.conf` |
| 그래픽 부팅 (systemd) | `graphical.target` (runlevel 5) |
| 텍스트 부팅 (systemd) | `multi-user.target` (runlevel 3) |
| 기본 부팅 모드 변경 | `systemctl set-default` |
| KDE 툴킷 | **Qt** |
| GNOME 툴킷 | **GTK+** |
| KDE 윈도우 매니저 | **Kwin** |
| GNOME 3 윈도우 매니저 | **Mutter** |
| XFCE 윈도우 매니저 | **Xfwm** |
| LXDE 윈도우 매니저 | **Openbox** |
| GNOME 디스플레이 매니저 | **GDM** |
| KDE Plasma 디스플레이 매니저 | **SDDM** |
| 모든 X 클라이언트 허용 | `xhost +` |
| 특정 호스트 허용 | `xhost +IP` |
| 쿠키 기반 X 인증 | `xauth` (MIT-MAGIC-COOKIE) |
| xauth 쿠키 확인 | `xauth list` |
| DISPLAY 형식 | `IP:디스플레이번호.스크린번호` |
| 저사양 경량 데스크톱 | **LXDE** |

## 관련 노트
- [[X-Windows Practice]]
- [[장치 설정]]
- [[셸 환경설정]]
- [[MOC - 리눅스마스터 2급]]
