---
keywords: exam traps, weak areas, common mistakes
---

# Exam Traps (시험 함정 포인트)

#dashboard #exam-traps

> [!warning] 이 노트의 목적
> 시험에서 자주 틀리거나 헷갈리는 포인트만 모은 **오답/함정 노트**입니다.

## 파일 권한과 소유권

> [!danger]- Trap: SetUID와 SetGID 숫자 혼동
> - SetUID = **4**000, SetGID = **2**000, Sticky bit = **1**000
> - `chmod 4755`는 SetUID, `chmod 2755`는 SetGID
> - 소문자 `s`(실행권한 있음) vs 대문자 `S`(실행권한 없음) 구분 필수
> - [[파일 권한과 소유권]]

> [!danger]- Trap: chmod 숫자 계산 실수
> - r=4, w=2, x=1 → `rwxr-xr--` = 754 (750이 아님!)
> - 특수권한 포함 시 4자리: `4755` = SetUID + rwxr-xr-x
> - [[파일 권한과 소유권]]

## 셸

> [!danger]- Trap: 셸 계열 분류 혼동
> - **본셸 계열**: sh, ksh, **bash**, zsh
> - **C셸 계열**: csh, tcsh
> - bash가 C셸이라고 착각하면 안 됨! bash = **B**ourne **A**gain **Sh**ell
> - [[셸의 종류와 특징]]

> [!danger]- Trap: /etc/profile vs ~/.bash_profile
> - `/etc/profile` = **전체** 사용자에 적용
> - `~/.bash_profile` = **개인** 사용자에만 적용
> - `/etc/bashrc` = alias, 함수 (환경변수 아님!)
> - [[셸 환경설정]]

## 프로세스 관리

> [!danger]- Trap: nice 값 범위와 의미
> - 범위: **-20**(가장 높은 우선순위) ~ **19**(가장 낮은 우선순위)
> - 값이 작을수록 우선순위가 **높음** (직관과 반대!)
> - 일반 사용자는 nice 값을 **높이기만** 가능 (우선순위 낮추기만)
> - [[프로세스 관리]]

> [!danger]- Trap: kill 시그널 번호
> - `-9` (SIGKILL) = **강제** 종료 (무시 불가)
> - `-15` (SIGTERM) = **정상** 종료 (기본값)
> - `-2` (SIGINT) = Ctrl+C와 동일
> - 기본 시그널이 `-15`임을 잊고 `-9`를 답으로 쓰지 않도록!
> - [[프로세스 관리]]

## 에디터

> [!danger]- Trap: vi 모드 전환 키 혼동
> - `i`(커서 앞 삽입) vs `a`(커서 뒤 삽입) vs `o`(아래 줄 삽입)
> - `O`(위 줄 삽입)와 `o`(아래 줄 삽입) 대소문자 구분
> - `dd`(삭제) vs `yy`(복사) — 둘 다 줄 단위
> - [[에디터]]

## 소프트웨어 설치

> [!danger]- Trap: RPM vs YUM 차이
> - RPM = 로컬 설치 (의존성 해결 **안 됨**)
> - YUM = 온라인 설치 (의존성 **자동 해결**)
> - 문제에서 "의존성"이 언급되면 → YUM 또는 APT-GET
> - [[소프트웨어 설치 및 삭제]]

> [!danger]- Trap: 소스 설치 순서
> - 반드시 `./configure → make → make install` 순서
> - `make`와 `make install` 순서 바꾸면 안 됨!
> - `./configure` 빼먹으면 Makefile 없어서 make 실패
> - [[소프트웨어 설치 및 삭제]]

## 장치 설정

> [!danger]- Trap: CUPS vs LPRng
> - **CUPS** = 현재 표준 프린터 시스템, 포트 **631**, 웹 관리
> - **LPRng** = 레거시 시스템
> - 시험에서 포트 번호 물어보면 CUPS = 631
> - [[장치 설정]]

## X-Windows

> [!danger]- Trap: xhost vs xauth
> - `xhost` = **IP 기반** 인증 (보안 약함)
> - `xauth` = **토큰(MIT-MAGIC-COOKIE) 기반** 인증 (보안 강함)
> - "보안"이 키워드면 → xauth
> - [[X-Windows]]

> [!danger]- Trap: 부팅 타겟 혼동
> - `graphical.target` = runlevel **5** = GUI
> - `multi-user.target` = runlevel **3** = CLI
> - 숫자 3과 5를 바꿔서 답하지 않도록!
> - [[X-Windows]]

## 네트워크

> [!danger]- Trap: OSI 계층 번호 혼동
> - 7(응용)-6(표현)-5(세션)-4(전송)-3(네트워크)-2(데이터링크)-1(물리)
> - IP는 3계층(네트워크), TCP는 4계층(전송)
> - ARP는 **3계층** (2계층이 아님!)
> - [[네트워크 기초]]

> [!danger]- Trap: TCP vs UDP 구분
> - TCP = **연결지향**, **3-way handshaking**, 신뢰성 높음
> - UDP = **비연결**, 빠름, DNS/스트리밍에 사용
> - FTP, HTTP = TCP / DNS 질의 = UDP
> - [[네트워크 기초]]

> [!danger]- Trap: RAID 레벨 최소 디스크 수
> - RAID 0 = **2개** (스트라이핑, 안전성 없음)
> - RAID 1 = **2개** (미러링, 용량 50%)
> - RAID 5 = **3개** (패리티 분산)
> - RAID 5의 최소 디스크를 2개로 답하면 오답!
> - [[클러스터링과 스토리지]]

---

## Related
- [[MOC - 리눅스마스터 2급]] → Weak Areas 섹션
- [[빠른 참조]]
