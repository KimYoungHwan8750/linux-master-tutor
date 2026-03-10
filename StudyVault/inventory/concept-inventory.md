# 개념 인벤토리

> 학습 자료에서 자동 추출된 전체 테스트 가능 개념 목록.
> 커버리지 계산 및 퀴즈 대상 선정의 기준.

## 섹션별 개념 수

| 섹션 | 총 개념 | 테스트됨 | 미테스트 | 커버리지 |
|------|---------|---------|---------|---------|
| 01-파일시스템 | 36 | 0 | 36 | 0% |
| 02-셸 | 27 | 0 | 27 | 0% |
| 03-프로세스관리 | 19 | 0 | 19 | 0% |
| 04-에디터 | 13 | 0 | 13 | 0% |
| 05-소프트웨어설치 | 16 | 0 | 16 | 0% |
| 06-장치설정 | 13 | 0 | 13 | 0% |
| 07-X윈도우 | 17 | 0 | 17 | 0% |
| 08-인터넷활용 | 60 | 0 | 60 | 0% |
| **합계** | **201** | **0** | **201** | **0%** |

---

## 01-파일시스템

### 파일 권한과 소유권

- [ ] ls -l 파일 유형 식별자 7종 (-, d, l, b, c, p, s)
- [ ] 파일 권한 rwx 숫자 모드 (r=4, w=2, x=1)
- [ ] chmod 기호 모드 (u/g/o/a ±= rwx)
- [ ] chown 명령어 (소유자 변경)
- [ ] chgrp 명령어 (그룹 변경)
- [ ] umask 계산법 (파일 666, 디렉토리 777에서 차감)
- [ ] SetUID (4000, 실행 시 소유자 권한, passwd 예시)
- [ ] SetGID (2000, 실행 시 그룹 권한)
- [ ] Sticky Bit (1000, 삭제 제한, /tmp 예시)
- [ ] 특수 권한 표기 (소문자 s/t vs 대문자 S/T)

### 디스크 쿼타와 파일시스템

- [ ] 쿼타 개념 (하드 제한 vs 소프트 제한 vs 유예 기간)
- [ ] quotacheck 명령어
- [ ] quotaon / quotaoff 명령어
- [ ] edquota 명령어
- [ ] repquota 명령어
- [ ] ext2 / ext3 / ext4 파일시스템 비교
- [ ] XFS 파일시스템
- [ ] NFS (네트워크 파일 시스템)
- [ ] SMB / CIFS
- [ ] /etc/fstab 6개 필드 구조
- [ ] UUID와 blkid 명령어
- [ ] inode 개념
- [ ] 파일시스템 구조 (슈퍼블록, 블록 비트맵, inode 테이블 등)
- [ ] 하드링크 vs 심볼릭 링크
- [ ] ln / ln -s 명령어

### 파일시스템 관리 명령어

- [ ] mount / umount 명령어
- [ ] mount -t 옵션 (파일시스템 유형 지정)
- [ ] mount -o 옵션 (ro, rw, noexec 등)
- [ ] fdisk 명령어 (파티션 관리)
- [ ] fdisk 내부 명령 (p, n, d, t, w, q)
- [ ] mkfs / mke2fs 명령어
- [ ] fsck / e2fsck 명령어
- [ ] du 명령어 (디스크 사용량, -s, -h)
- [ ] df 명령어 (디스크 여유공간, -h, -i)
- [ ] dumpe2fs / tune2fs 명령어
- [ ] xfs_info / xfs_repair 명령어

---

## 02-셸

### 셸의 종류와 특징

- [ ] 본셸 (sh) — Stephen Bourne, Bell Labs, 최초 유닉스 셸
- [ ] 콘셸 (ksh) — David Korn, 본셸+C셸 결합
- [ ] 배쉬셸 (bash) — GNU, POSIX 호환, Bourne Again Shell
- [ ] 지셸 (zsh) — 강력한 히스토리/자동완성/플러그인
- [ ] C셸 (csh) — Bill Joy, C 언어 문법, 히스토리/별칭 최초 도입
- [ ] tc셸 (tcsh) — C셸 개선, 자동완성 추가
- [ ] /etc/shells 파일 (사용 가능한 셸 목록)
- [ ] chsh 명령어 (-s, -l 옵션)
- [ ] usermod -s (셸 변경)
- [ ] echo $SHELL (현재 셸 확인)

### 셸 환경설정

- [ ] env 명령어 (환경변수 목록)
- [ ] set 명령어 (셸+환경 변수 모두)
- [ ] export 명령어 (셸→환경변수 전환)
- [ ] printenv 명령어
- [ ] 셸 변수 vs 환경변수 구분
- [ ] 주요 환경변수 (PATH, HOME, SHELL, USER, HOSTNAME, LANG 등)
- [ ] PS1 특수문자 (\u, \h, \w, \$)
- [ ] PS2 보조 프롬프트
- [ ] /etc/profile (시스템 전체, 로그인 시)
- [ ] /etc/bashrc (시스템 전체, bash 실행 시)
- [ ] ~/.bash_profile (개인, 로그인 시)
- [ ] ~/.bashrc (개인, bash 실행 시)
- [ ] 로그인 셸 vs 비로그인 셸 (읽는 파일 차이)
- [ ] 설정 파일 적용 순서 (/etc/profile → ~/.bash_profile → ~/.bashrc → /etc/bashrc)
- [ ] history 명령어 (!!, !n, -c, -w)
- [ ] alias / unalias 명령어
- [ ] /etc/passwd 필드 구조 (7개 필드)

---

## 03-프로세스관리

- [ ] 프로세스 개념 (PID, PPID)
- [ ] 데몬(Daemon) 프로세스
- [ ] ps 명령어와 주요 옵션 (aux vs -ef)
- [ ] top 명령어
- [ ] kill 명령어
- [ ] 주요 시그널 (SIGHUP=1, SIGINT=2, SIGKILL=9, SIGTERM=15, SIGTSTP=20)
- [ ] killall / pkill 명령어
- [ ] nice 명령어 (NI값 설정)
- [ ] renice 명령어 (NI값 변경)
- [ ] NI값 범위 (-20~19, 일반 사용자 0~19)
- [ ] nohup 명령어
- [ ] & (백그라운드 실행)
- [ ] jobs / fg / bg 명령어
- [ ] cron 데몬과 crontab 명령어 (-e, -l, -r, -u)
- [ ] crontab 필드 형식 (분 시 일 월 요일 명령)
- [ ] at 명령어
- [ ] /etc/cron.allow, /etc/cron.deny
- [ ] 포그라운드 vs 백그라운드 프로세스
- [ ] 좀비 프로세스 / 고아 프로세스

---

## 04-에디터

- [ ] vi 3가지 모드 (명령, 입력, 라인명령)
- [ ] vi 입력 모드 전환 (i, a, o, I, A, O)
- [ ] vi 커서 이동 (h, j, k, l)
- [ ] vi 삭제 명령 (x, dd, dw, D)
- [ ] vi 복사/붙여넣기 (yy, p, P)
- [ ] vi 되돌리기 (u, Ctrl+r)
- [ ] vi 검색 (/, ?, n, N)
- [ ] vi 치환 (:s, :%s)
- [ ] vi 저장/종료 (:w, :q, :wq, :q!, ZZ)
- [ ] vi set 명령 (:set nu, :set ai 등)
- [ ] vi 라인 이동 (G, gg, :n)
- [ ] emacs 편집기 (특징, 주요 키바인딩)
- [ ] nano / pico 편집기

---

## 05-소프트웨어설치

- [ ] RPM 패키지 관리 (설치 -i/-ivh, 제거 -e, 업그레이드 -U/-F)
- [ ] rpm 질의 옵션 (-q, -qa, -qi, -ql, -qf)
- [ ] rpm 검증 (-V)
- [ ] YUM (yum install/remove/update)
- [ ] yum list / info / search
- [ ] yum 설정 파일 (/etc/yum.conf, /etc/yum.repos.d/)
- [ ] DNF (YUM 후속)
- [ ] dpkg 패키지 관리 (-i, -r, -P, -l, -L, -s)
- [ ] APT (apt-get install/remove/update/upgrade)
- [ ] apt-cache search / show
- [ ] /etc/apt/sources.list
- [ ] zypper (SUSE)
- [ ] 소스 코드 설치 3단계 (configure → make → make install)
- [ ] tar 명령어 옵션 (-c, -x, -t, -f, -v, -z, -j, -J)
- [ ] gzip / bzip2 / xz 압축 비교
- [ ] RPM vs DPKG, YUM vs APT 비교

---

## 06-장치설정

- [ ] LPRng (BSD 인쇄, /etc/printcap)
- [ ] CUPS (애플, HTTP/IPP, 포트 631)
- [ ] CUPS 설정 파일 (/etc/cups/cupsd.conf, printers.conf 등)
- [ ] BSD 프린터 명령어 (lpr, lpq, lprm, lpc)
- [ ] System V 프린터 명령어 (lp, lpstat, cancel)
- [ ] BSD vs System V 명령어 비교 (-P vs -d, -# vs -n)
- [ ] OSS (유닉스 사운드, POSIX)
- [ ] ALSA (리눅스 커널 사운드)
- [ ] alsactl / alsamixer 명령어
- [ ] cdparanoia 명령어 (CD 오디오 추출)
- [ ] SANE (스캐너 API, 백엔드/프론트엔드)
- [ ] XSANE (SANE GUI 프론트엔드)
- [ ] sane-find-scanner / scanimage / scanadf / xcam 명령어

---

## 07-X윈도우

- [ ] X-Windows 기본 개념 (네트워크 기반, 클라이언트/서버, MIT)
- [ ] X서버 vs X클라이언트 (일반 네트워크와 반대 구조)
- [ ] X프로토콜 4가지 메시지 (Request, Reply, Error, Event)
- [ ] Xlib / XCB / Xtoolkit 라이브러리
- [ ] XFree86 (XF86Config) vs Xorg (xorg.conf)
- [ ] xorg.conf 주요 섹션 (ServerLayout, Files, Module, InputDevice, Monitor, Device, Screen)
- [ ] systemd target vs SysV runlevel 비교
- [ ] graphical.target = runlevel 5, multi-user.target = runlevel 3
- [ ] systemctl set-default / get-default / isolate
- [ ] 윈도우 매니저 (Metacity, Mutter, Kwin, Xfwm, Openbox 등)
- [ ] 데스크톱 환경 (KDE/Qt, GNOME/GTK+, LXDE, XFCE)
- [ ] 추가 데스크톱 환경 (Cinnamon, MATE, Unity, Budgie)
- [ ] 디스플레이 매니저 (XDM, GDM, KDM, SDDM, LightDM, LXDM)
- [ ] xhost 명령어 (+, -, +IP, -IP)
- [ ] xauth 명령어 (MIT-MAGIC-COOKIE, ~/.Xauthority)
- [ ] xhost vs xauth 비교 (호스트 기반 vs 쿠키 기반)
- [ ] DISPLAY 환경변수 형식 (IP:디스플레이번호.스크린번호)

---

## 08-인터넷활용

### 네트워크 기초

- [ ] LAN / MAN / WAN / SAN 비교
- [ ] LAN 기술 (Ethernet, Token Ring, FDDI)
- [ ] 토폴로지: 성형(Star) — 중앙 장치 고장 시 전체 마비
- [ ] 토폴로지: 망형(Mesh) — 신뢰성 최고, 비용 높음
- [ ] 토폴로지: 버스형(Bus) — 비용 저렴, 병목
- [ ] 토폴로지: 링형(Ring) — 노드 장애 시 전체 영향
- [ ] 토폴로지: 트리형(Tree) — 계층 구조
- [ ] OSI 7계층 이름과 순서
- [ ] 계층별 데이터 단위 (Bit, Frame, Packet, Segment, Data)
- [ ] 계층별 주요 장비 (리피터, 허브, 브릿지, 스위치, 라우터, 게이트웨이)
- [ ] IP / ICMP / IGMP 프로토콜
- [ ] ARP (IP→MAC) vs RARP (MAC→IP)
- [ ] TCP vs UDP 상세 비교
- [ ] TCP 3-Way Handshake (SYN → SYN+ACK → ACK)
- [ ] TCP 4-Way Handshake (FIN → ACK → FIN → ACK)
- [ ] TCP 주요 상태 (LISTEN, ESTABLISHED, TIME_WAIT 등)
- [ ] IPv4 클래스 A/B/C/D/E 범위
- [ ] 특수 IP 주소 / 사설 IP 대역
- [ ] IPv4(32bit) / IPv6(128bit) / MAC(48bit) 크기
- [ ] 서브넷 마스크와 CIDR 표기법
- [ ] 국제 기구 (ICANN, IEEE, ISO, IETF, W3C)

### 네트워크 명령어와 서비스

- [ ] 주요 서비스별 포트 번호 (FTP 21, SSH 22, Telnet 23, SMTP 25, DNS 53, HTTP 80, POP3 110, IMAP 143, HTTPS 443)
- [ ] ifconfig 명령어 (인터페이스 설정/확인)
- [ ] ip 명령어 (ip addr, ip link, ip route, ip neigh)
- [ ] nslookup 명령어 (DNS 질의)
- [ ] ping 명령어 (ICMP, -c, -i, -s 옵션)
- [ ] traceroute 명령어 (경로 추적)
- [ ] netstat 명령어 (-a, -n, -t, -u, -l, -p, -r)
- [ ] ss 명령어 (netstat 대체)
- [ ] route 명령어 (라우팅 테이블)
- [ ] ethtool / mii-tool 명령어
- [ ] arp 명령어 (ARP 테이블)
- [ ] 레거시 vs 현대 네트워크 명령어 대응표
- [ ] WWW (HTTP/HTTPS)
- [ ] Gopher (미네소타 대학, 텍스트 기반)
- [ ] 전자 메일 (SMTP 송신 / POP3 수신 다운로드 / IMAP 수신 서버 보관)
- [ ] FTP / SFTP / FTPS
- [ ] Telnet vs SSH
- [ ] IRC (실시간 채팅)
- [ ] SAMBA (Windows-Linux 공유, SMB/CIFS)
- [ ] DNS (/etc/resolv.conf, 포트 53)
- [ ] 주요 설정 파일 (/etc/hosts, /etc/resolv.conf, /etc/hostname, /etc/services)

### 클러스터링과 스토리지

- [ ] RAID 0 (스트라이핑, 속도↑, 복구 불가)
- [ ] RAID 1 (미러링, 2배 용량, 백업)
- [ ] RAID 5 (스트라이핑+패리티, 최소 3개, 실무 다용)
- [ ] RAID 6 / RAID 1+0
- [ ] LVM 개념과 구조 (PV → VG → LV)
- [ ] LVM 구성 요소 (PV, VG, LV, PE)
- [ ] LVM 명령어 (pvcreate/vgcreate/lvcreate, pvdisplay/vgdisplay/lvdisplay)
- [ ] LVM 확장/축소 (lvextend/lvreduce/vgextend/vgreduce)
- [ ] HPC 클러스터 (고성능 계산, 베어울프)
- [ ] LVS 클러스터 (부하 분산, 로드밸런서)
- [ ] HA 클러스터 (고가용성, IP 이주)
- [ ] Xen (반가상화) vs KVM (전가상화)
- [ ] VirtualBox (오라클, 독자적 가상 장치)
- [ ] Docker (컨테이너 기반)
- [ ] 전가상화 vs 반가상화 비교
- [ ] 하이퍼바이저 Type 1 (베어메탈) vs Type 2 (호스트형)
- [ ] IaaS / PaaS / SaaS
- [ ] 하둡 (Hadoop, 자바, HDFS, MapReduce)
