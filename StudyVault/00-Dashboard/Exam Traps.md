---
keywords: exam traps, weak areas, common mistakes
---

# 시험 함정 포인트

#dashboard #exam-traps #linux-master

> [!warning] 이 노트의 목적
> 시험에서 자주 틀리거나 헷갈리는 포인트만 모은 **오답/함정 노트**입니다.

---

## 파일시스템

> [!danger]- 함정: umask 계산 실수
> - umask는 **빼기** 연산: 파일(`666 - umask`), 디렉토리(`777 - umask`)
> - 파일 기본 최대 권한이 **666**임을 잊으면 계산 틀림
> - 예: umask 022 → 파일 644, 디렉토리 755
> - [[파일 권한과 소유권]]

> [!danger]- 함정: Sticky Bit 적용 대상
> - Sticky Bit(1000)은 **디렉토리에만** 의미 있음
> - 디렉토리에 설정하면 소유자만 삭제 가능 (예: `/tmp`)
> - SetUID/SetGID와 혼동하지 말 것
> - [[파일 권한과 소유권]]

> [!danger]- 함정: SetUID의 s vs S
> - 소문자 `s`: 기존 실행 권한(x)이 **있는** 상태에서 SetUID 부여
> - 대문자 `S`: 기존 실행 권한(x)이 **없는** 상태에서 SetUID 부여
> - `S`는 SetUID가 설정되었지만 실행 권한이 없어 사실상 무의미
> - [[파일 권한과 소유권]]

> [!danger]- 함정: chgrp vs chown 혼동
> - `chgrp`: **그룹만** 변경
> - `chown`: 소유자 변경 (소유자:그룹 형태로 그룹도 변경 가능)
> - `chown :group file` = `chgrp group file`
> - [[파일 권한과 소유권]]

> [!danger]- 함정: du vs df 혼동
> - `du` (disk usage): 디렉토리별 **사용량** 확인
> - `df` (disk free): 파일시스템 **여유 공간** 확인
> - 이름의 약자를 기억: **u**sage vs **f**ree
> - [[파일시스템 관리 명령어]]

> [!danger]- 함정: ext2 vs ext3 저널링
> - `ext2`: **비저널링** (저널링 없음)
> - `ext3`: **저널링** 지원 + ACL 지원
> - `ext4`: ext3 호환 + 대용량 지원
> - 저널링 유무가 가장 큰 차이점
> - [[디스크 쿼타와 파일시스템]]

---

## 셸

> [!danger]- 함정: bash vs csh 계보 혼동
> - `bash`: **GNU** 프로젝트, **POSIX** 호환, Bourne 계열
> - `csh`: **Bill Joy**, **UC Berkeley**, C 언어 문법 기반
> - `ksh`: AT&T, David Korn → Bourne 계열
> - bash가 C 셸이라고 착각하지 말 것
> - [[셸의 종류와 특징]]

> [!danger]- 함정: /etc/profile vs /etc/bashrc 시점
> - `/etc/profile`: **로그인 시** 실행 (전체 사용자)
> - `/etc/bashrc`: **셸 실행 시** 실행 (전체 사용자)
> - `~/.bash_profile`: 로그인 시 (개인)
> - `~/.bashrc`: 셸 실행 시 (개인)
> - "로그인"과 "실행"의 차이를 구분할 것
> - [[셸 환경설정]]

> [!danger]- 함정: PS1 vs PS2 프롬프트
> - `PS1`: **주 프롬프트** (기본 입력 대기)
> - `PS2`: **보조 프롬프트** (연속 입력, 기본값 `>`)
> - PS2는 명령이 완성되지 않았을 때 표시됨
> - [[셸 환경설정]]

---

## 프로세스 관리

> [!danger]- 함정: kill 기본 시그널
> - `kill` 명령의 기본 시그널은 **15 (SIGTERM)** — 정상 종료 요청
> - **9 (SIGKILL)**는 강제 종료 — 프로세스가 무시 불가
> - `kill PID` ≠ 강제 종료! `-9` 옵션을 줘야 강제 종료
> - [[프로세스 관리]]

> [!danger]- 함정: nice 값 방향
> - nice 값이 **낮을수록** 우선순위가 **높음**
> - 범위: **-20** (최고 우선순위) ~ **19** (최저 우선순위)
> - 기본값: **0**
> - 일반 사용자는 nice 값을 높일 수만 있음 (우선순위 낮추기만 가능)
> - root만 음수 값 설정 가능
> - [[프로세스 관리]]

> [!danger]- 함정: standalone vs inetd(xinetd) 방식
> - **standalone**: 항상 메모리에 상주, 빠른 응답 (httpd, sendmail)
> - **inetd/xinetd**: 요청 시에만 실행, 메모리 절약 (telnet, ftp)
> - xinetd는 inetd의 확장판 (보안 기능 추가)
> - [[프로세스 관리]]

---

## 에디터

> [!danger]- 함정: vi 입력 모드 진입 키
> - `i`: 커서 **앞**에 삽입
> - `a`: 커서 **뒤**에 삽입
> - `o`: 현재 줄 **아래**에 새 줄 삽입
> - `I`: 행 **처음**에 삽입
> - `A`: 행 **끝**에 삽입
> - `O`: 현재 줄 **위**에 새 줄 삽입
> - i/a 방향, o/O 방향을 헷갈리기 쉬움
> - [[에디터]]

> [!danger]- 함정: :wq vs :q! vs ZZ
> - `:wq` — 저장 후 종료
> - `:q!` — 저장하지 않고 **강제** 종료
> - `ZZ` — `:wq`와 동일 (명령 모드에서 Shift+Z+Z)
> - `:w` — 저장만 (종료 안 함)
> - `:q` — 변경 없을 때만 종료 가능
> - [[에디터]]

> [!danger]- 함정: crontab 요일 번호
> - **0** = 일요일, **1** = 월요일, ..., **6** = 토요일
> - **7** = 일요일 (0과 동일, 일부 시스템)
> - 0이 일요일이라는 점을 잊기 쉬움
> - crontab 형식: `분 시 일 월 요일 명령`
> - [[프로세스 관리]]

---

## 소프트웨어 설치

> [!danger]- 함정: rpm -U vs -F
> - `-U` (Upgrade): 패키지가 **없으면 설치**, 있으면 업그레이드
> - `-F` (Freshen): 패키지가 **있을 때만** 업그레이드 (없으면 무시)
> - `-i`는 순수 설치 (이미 있으면 에러)
> - [[소프트웨어 설치 및 삭제]]

> [!danger]- 함정: dpkg -r vs -P
> - `-r` (remove): 패키지 삭제 (설정파일 **유지**)
> - `-P` (purge): 패키지 + **설정파일까지** 완전 삭제
> - 설정파일 보존 여부가 핵심 차이
> - [[소프트웨어 설치 및 삭제]]

> [!danger]- 함정: 압축 효율 순서
> - **xz > bzip2 > gzip > compress**
> - 효율이 높을수록 압축/해제 시간은 더 걸림
> - [[소프트웨어 설치 및 삭제]]

> [!danger]- 함정: tar 압축 옵션 혼동
> - `-J`: **xz** (.tar.xz)
> - `-j`: **bzip2** (.tar.bz2)
> - `-z`: **gzip** (.tar.gz)
> - `-Z`: **compress** (.tar.Z)
> - 대문자 J=xz, 소문자 j=bzip2를 헷갈리기 쉬움
> - [[소프트웨어 설치 및 삭제]]

---

## 장치 설정

> [!danger]- 함정: LPRng vs CUPS 구분
> - **LPRng**: BSD 계열 인쇄 시스템, 설정파일 `/etc/printcap`
> - **CUPS**: 애플 개발, IPP 프로토콜, 설정 `/etc/cups/`, 웹관리 `localhost:631`
> - CUPS가 현재 표준이지만, LPRng 관련 문제도 출제됨
> - [[장치 설정]]

> [!danger]- 함정: BSD 명령 vs SysV 명령
> - BSD: `lpr`(인쇄), `lpq`(큐), `lprm`(삭제), `lpc`(제어)
> - SysV: `lp`(인쇄), `lpstat`(상태), `cancel`(취소)
> - `lpr` vs `lp`, `lpq` vs `lpstat` — 계열이 다른 명령어 쌍
> - [[장치 설정]]

> [!danger]- 함정: OSS vs ALSA
> - **OSS**: Open Sound System, **POSIX** 기반 사운드 아키텍처
> - **ALSA**: Advanced Linux Sound Architecture, **커널** 요소, 자동 구성
> - ALSA가 OSS를 대체했으며, OSS 호환 모듈 제공
> - [[장치 설정]]

---

## X-Windows

> [!danger]- 함정: graphical.target vs multi-user.target
> - `graphical.target` = **런레벨 5** (GUI)
> - `multi-user.target` = **런레벨 3** (텍스트/CLI)
> - systemd 타겟명과 전통 런레벨 번호 매핑을 외울 것
> - [[X-Windows]]

> [!danger]- 함정: KDE=Qt vs GNOME=GTK+ 혼동
> - **KDE**: **Qt** 툴킷 (노키아), 윈도우 매니저 **Kwin**
> - **GNOME**: **GTK+** 툴킷 (GNU), 윈도우 매니저 **Mutter**
> - Qt와 GTK+를 반대로 기억하기 쉬움
> - LXDE와 XFCE는 모두 GTK+ 사용
> - [[X-Windows]]

> [!danger]- 함정: xhost vs xauth 방식
> - `xhost`: **호스트(IP)** 기반 접근 제어 — 보안 약함
> - `xauth`: **쿠키** 기반 인증 (MIT-MAGIC-COOKIE-1) — 보안 강함
> - xhost는 호스트 단위, xauth는 사용자 단위 인증
> - [[X-Windows]]

> [!danger]- 함정: DISPLAY 환경변수 형식
> - `export DISPLAY=호스트IP:디스플레이번호.스크린번호`
> - 예: `export DISPLAY=192.168.1.1:0.0`
> - 로컬: `export DISPLAY=:0.0`
> - 콜론(:) 앞이 호스트, 뒤가 디스플레이.스크린
> - [[X-Windows]]

---

## 인터넷 활용

> [!danger]- 함정: ARP vs RARP 방향
> - **ARP**: IP 주소 → **MAC** 주소 (IP를 알 때 MAC을 찾음)
> - **RARP**: MAC 주소 → **IP** 주소 (MAC을 알 때 IP를 찾음)
> - A=Address, R=Reverse — "R이 붙으면 반대 방향"
> - [[네트워크 기초]]

> [!danger]- 함정: TCP vs UDP 프로토콜 구분
> - **TCP**: 연결 지향, 신뢰성, 느림 (HTTP, FTP, SMTP, SSH)
> - **UDP**: 비연결, 비신뢰성, 빠름 (DNS, DHCP, SNMP, TFTP)
> - DNS는 기본 UDP이지만 영역 전송 시 TCP도 사용 (53번 포트)
> - [[네트워크 기초]]

> [!danger]- 함정: 3-Way vs 4-Way Handshake
> - **3-Way** (연결): SYN → SYN+ACK → ACK
> - **4-Way** (종료): FIN → ACK → FIN → ACK
> - 연결은 3단계, 종료는 4단계 — 숫자 혼동 주의
> - [[네트워크 기초]]

> [!danger]- 함정: RAID 레벨 특성
> - **RAID 0**: 스트라이핑, 성능 향상, **복구 불가** (결함 허용 없음)
> - **RAID 1**: 미러링, 동일 데이터 복제, 복구 가능
> - **RAID 5**: 스트라이핑 + 분산 패리티, 1개 디스크 장애 허용
> - RAID 0은 "안전"하지 않다는 점을 잊기 쉬움
> - [[클러스터링과 스토리지]]

> [!danger]- 함정: LVM 구성 순서
> - **PV** (Physical Volume) → **VG** (Volume Group) → **LV** (Logical Volume)
> - 물리 → 그룹 → 논리 순서
> - 명령어도 순서대로: `pvcreate` → `vgcreate` → `lvcreate`
> - [[클러스터링과 스토리지]]

> [!danger]- 함정: IaaS vs PaaS vs SaaS
> - **IaaS**: 하드웨어/인프라 제공 (AWS EC2, OpenStack)
> - **PaaS**: 개발 플랫폼 제공 (Heroku, Google App Engine)
> - **SaaS**: 완성된 애플리케이션 제공 (Google Docs, Office 365)
> - 제공 범위: IaaS < PaaS < SaaS (사용자 관리 부담은 반대)
> - [[클러스터링과 스토리지]]

---

## 관련
- [[MOC - 리눅스마스터 2급]] → 취약 영역 섹션
- [[빠른 참조]]
