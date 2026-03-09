---
source_pdf: 원문 미보유 (웹 소스)
part: Part 3 Ch01
keywords: x-windows, x-server, desktop, xhost, xauth
---

# X-Windows (★★)

#x-windows #linux-master

## Overview Table (한눈에 비교)
| 항목 | 내용 |
|------|------|
| 구조 | 클라이언트-서버 모델 (네트워크 투명성) |
| X서버 | 화면 출력, 입력 처리 (사용자 측) |
| X클라이언트 | 응용 프로그램 (서버 측에서 실행 가능) |
| 실행 | `startx` |

## X서버와 X클라이언트

```
┌──────────────────┐      네트워크       ┌──────────────────┐
│   X 클라이언트    │ ←──────────────→  │    X 서버         │
│ (응용 프로그램)    │   X 프로토콜      │ (디스플레이 장치)  │
│ 원격 머신에서 실행 │                   │ 사용자 앞에 위치   │
└──────────────────┘                   └──────────────────┘
```

> [!warning] 서버/클라이언트 혼동 주의
> 일반적인 웹과 **반대** 개념! X서버가 사용자 앞(화면), X클라이언트가 원격(앱 실행).

## 부팅 모드 (Run Level / Target)

| 모드 | systemd target | 런레벨 | 설명 |
|------|---------------|--------|------|
| GUI | `graphical.target` | 5 | X-Windows 포함 부팅 |
| CLI | `multi-user.target` | 3 | 텍스트 모드 부팅 |

```bash
# 기본 부팅 모드 변경
systemctl set-default graphical.target   # GUI
systemctl set-default multi-user.target  # CLI

# 현재 부팅 모드 확인
systemctl get-default
```

## 윈도우 매니저 (Window Manager)

| WM | 특징 |
|----|------|
| fvwm | 가벼운 윈도우 매니저 |
| twm | X11 기본 제공 WM |
| Kwin | KDE 기본 WM |
| Mutter | GNOME 기본 WM |

## 데스크톱 환경 (Desktop Environment)

| DE | 툴킷 | 특징 |
|----|-------|------|
| **KDE** | Qt | 기능 풍부, 커스터마이징 |
| **GNOME** | GTK | 직관적, 깔끔한 UI |
| **XFCE** | GTK | 경량, 중간 성능 |
| **LXDE** | GTK | 초경량, 구형 하드웨어용 |

> [!tip] 툴킷 구분
> KDE만 **Qt**, 나머지(GNOME, XFCE, LXDE)는 모두 **GTK** 사용

## X-Windows 인증

| 방식 | 명령어 | 보안 | 원리 |
|------|--------|------|------|
| **xhost** | `xhost +hostname` | 약함 | IP 기반 접근 제어 |
| **xauth** | `xauth` | 강함 | MIT-MAGIC-COOKIE 토큰 기반 |

```bash
xhost +192.168.1.100     # 특정 IP 허용
xhost +                  # 모든 호스트 허용 (보안 위험!)
xhost -                  # 접근 제어 활성화
```

> [!warning] xhost + 사용 주의
> `xhost +`는 모든 호스트를 허용하므로 **보안상 매우 위험**!

## DISPLAY 변수

```bash
export DISPLAY=hostname:displaynumber.screennumber
export DISPLAY=192.168.1.100:0.0
```

---

## Exam/Test Patterns (시험 빈출 패턴)
| Scenario/Keyword | Answer |
|-------------------|--------|
| "X-Windows 실행 명령" | **startx** |
| "GUI 부팅 타겟" | **graphical.target** (runlevel 5) |
| "CLI 부팅 타겟" | **multi-user.target** (runlevel 3) |
| "보안 강한 X 인증" | **xauth** (MIT-MAGIC-COOKIE) |
| "IP 기반 X 인증" | **xhost** |
| "KDE 사용 툴킷" | **Qt** |
| "GNOME 사용 툴킷" | **GTK** |
| "경량 데스크톱" | **XFCE** 또는 **LXDE** |

## Related Notes
- [[장치 설정]]
- [[네트워크 기초]]
