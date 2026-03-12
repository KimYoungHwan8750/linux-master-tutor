# X윈도우 — 개념 추적

| 개념 | 시도 | 정답 | 최종 테스트 | 상태 |
|------|------|------|------------|------|
| X서버 vs X클라이언트 (일반 네트워크와 반대 구조) | 1 | 1 | 2026-03-12 | 🟢 |
| systemd target vs SysV runlevel 비교 | 1 | 0 | 2026-03-12 | 🔴 |
| 데스크톱 환경 (KDE/Qt, GNOME/GTK+, LXDE, XFCE) | 1 | 0 | 2026-03-12 | 🔴 |
| xhost 명령어 (+, -, +IP, -IP) | 1 | 1 | 2026-03-12 | 🟢 |
| DISPLAY 환경변수 형식 (IP:디스플레이번호.스크린번호) | 1 | 0 | 2026-03-12 | 🔴 |
| X프로토콜 4가지 메시지 (Request, Reply, Error, Event) | 1 | 1 | 2026-03-12 | 🟢 |
| 윈도우 매니저 (Metacity, Mutter, Kwin, Xfwm, Openbox 등) | 1 | 0 | 2026-03-12 | 🔴 |
| xauth 명령어 (MIT-MAGIC-COOKIE, ~/.Xauthority) | 1 | 1 | 2026-03-12 | 🟢 |
| 디스플레이 매니저 (XDM, GDM, KDM, SDDM, LightDM, LXDM) | 1 | 0 | 2026-03-12 | 🔴 |

### 오답 메모

**systemd target vs SysV runlevel**
- 문제: 그래픽 모드의 target과 runlevel은?
- 내 답: 모름
- 정답: graphical.target / runlevel 5
- 핵심: 텍스트=multi-user.target=runlevel 3, 그래픽=graphical.target=runlevel 5.

**데스크톱 환경 (KDE/Qt)**
- 문제: KDE가 사용하는 GUI 툴킷은?
- 내 답: GTK+
- 정답: Qt
- 핵심: KDE=Qt, GNOME/XFCE/LXDE=GTK+. KDE만 유일하게 Qt 사용.

**DISPLAY 환경변수**
- 문제: DISPLAY 환경변수의 형식은?
- 내 답: 프로토콜://IP:포트
- 정답: IP:디스플레이번호.스크린번호
- 핵심: URL 형식 아님. 콜론(:) 뒤 디스플레이번호, 점(.) 뒤 스크린번호. 예: 192.168.1.100:0.0

**윈도우 매니저**
- 문제: GNOME 3에서 기본으로 사용하는 윈도우 매니저는?
- 내 답: Kwin
- 정답: Mutter
- 핵심: GNOME 2=Metacity, GNOME 3=Mutter(후속), KDE=Kwin, XFCE=Xfwm, LXDE=Openbox.

**디스플레이 매니저**
- 문제: KDE Plasma 5 이상에서 KDM을 대체하는 디스플레이 매니저는?
- 내 답: 모름
- 정답: SDDM (Simple Desktop Display Manager)
- 핵심: GDM=GNOME, KDM=KDE 4이하, SDDM=KDE Plasma 5+, LightDM=경량 범용, LXDM=LXDE.
