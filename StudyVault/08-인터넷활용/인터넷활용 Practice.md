---
source_pdf: programjy.tistory.com
part: "리눅스마스터 2급 2차 - 인터넷활용 Practice"
keywords: practice, network, RAID, LVM, cluster, virtualization, cloud
---

# 인터넷활용 Practice (12문제)

#practice #network

## 관련 개념
- [[네트워크 기초]]
- [[네트워크 명령어와 서비스]]
- [[클러스터링과 스토리지]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | IP → MAC 변환 | ARP |
> | MAC → IP 변환 | RARP |
> | OSI 3계층 장비 | 라우터 |
> | TCP 연결 설정 | 3-Way Handshake |
> | RAID 0 | 스트라이핑, 복구 불가 |
> | RAID 1 | 미러링, 2배 용량 |
> | RAID 5 | 패리티, 최소 3개 |
> | LVM 순서 | PV → VG → LV |
> | 반가상화 | Xen |
> | 전가상화 (레드햇) | KVM |
> | IaaS 예시 | Amazon EC2 |

---

## 문제 1 - OSI 7계층 [recall]
> 다음 OSI 7계층의 빈칸을 채우시오.
> | 계층 | 이름 | 데이터 단위 | 대표 장비 |
> |------|------|-------------|-----------|
> | 7 | 응용 | (가) | 게이트웨이 |
> | 4 | (나) | Segment | (다) |
> | 3 | 네트워크 | (라) | (마) |
> | 2 | (바) | Frame | (사) |
> | 1 | 물리 | (아) | 리피터, 허브 |

> [!answer]- 정답 보기
> | 빈칸 | 정답 |
> |------|------|
> | (가) | **Data** |
> | (나) | **전송 (Transport)** |
> | (다) | **게이트웨이** |
> | (라) | **Packet** |
> | (마) | **라우터** |
> | (바) | **데이터링크 (Data Link)** |
> | (사) | **스위치 / 브릿지** |
> | (아) | **Bit** |
>
> 기억법: 데이터 단위 - "**Bit → Frame → Packet → Segment → Data**" (물데네전~)

---

## 문제 2 - ARP / RARP [recall]
> (1) IP 주소를 알고 MAC 주소를 모를 때 사용하는 프로토콜은?
> (2) MAC 주소를 알고 IP 주소를 모를 때 사용하는 프로토콜은?

> [!answer]- 정답 보기
> | 번호 | 프로토콜 | 변환 |
> |------|----------|------|
> | (1) | **ARP** (Address Resolution Protocol) | **IP → MAC** |
> | (2) | **RARP** (Reverse ARP) | **MAC → IP** |
>
> ARP는 **A**ddress(IP)로부터 MAC을 찾고, **R**ARP는 **R**everse(반대)로 MAC에서 IP를 찾는다.

---

## 문제 3 - TCP vs UDP [recall]
> TCP와 UDP의 차이점을 연결 방식, 신뢰성, 속도, 대표 서비스 측면에서 비교하시오.

> [!answer]- 정답 보기
> | 구분 | TCP | UDP |
> |------|-----|-----|
> | 연결 방식 | **연결 지향** | **비연결** |
> | 신뢰성 | 높음 (전달 보장) | 낮음 (보장 안 함) |
> | 순서 보장 | O | X |
> | 속도 | 느림 | **빠름** |
> | 대표 서비스 | FTP, HTTP, SMTP, Telnet | **DNS**, DHCP, SNMP |
>
> TCP는 3-Way Handshake로 연결을 설정한 후 데이터를 전송한다.

---

## 문제 4 - TCP 3-Way Handshake [recall]
> TCP 연결 설정에 사용되는 3-Way Handshake의 각 단계를 플래그와 방향을 포함하여 서술하시오.

> [!answer]- 정답 보기
> | 단계 | 방향 | 플래그 | 설명 |
> |------|------|--------|------|
> | 1 | 클라이언트 → 서버 | **SYN** | 연결 요청 |
> | 2 | 서버 → 클라이언트 | **SYN + ACK** | 연결 수락 + 확인 |
> | 3 | 클라이언트 → 서버 | **ACK** | 연결 확인 완료 |
>
> 연결 해제는 **4-Way Handshake**: FIN → ACK → FIN → ACK

---

## 문제 5 - 포트 번호 [recall]
> 다음 서비스의 기본 포트 번호를 적으시오.
> (1) FTP (2) SSH (3) Telnet (4) SMTP (5) DNS (6) HTTP (7) POP3 (8) HTTPS

> [!answer]- 정답 보기
> | 서비스 | 포트 |
> |--------|------|
> | (1) FTP | **21** |
> | (2) SSH | **22** |
> | (3) Telnet | **23** |
> | (4) SMTP | **25** |
> | (5) DNS | **53** |
> | (6) HTTP | **80** |
> | (7) POP3 | **110** |
> | (8) HTTPS | **443** |

---

## 문제 6 - 네트워크 명령어 [application]
> 관리자가 서버의 네트워크 상태를 점검하려 한다. 다음 상황에 적합한 명령어를 적으시오.
> (1) 특정 호스트와의 통신 여부 확인 (ICMP 사용)
> (2) 목적지까지의 패킷 경로 추적
> (3) 현재 TCP 연결 중 LISTEN 상태인 포트와 PID 확인

> [!answer]- 정답 보기
> | 번호 | 명령어 | 설명 |
> |------|--------|------|
> | (1) | `ping 호스트` | ICMP 기반 통신 점검 |
> | (2) | `traceroute 호스트` | 패킷 경로 추적 |
> | (3) | `netstat -tlnp` 또는 `ss -tlnp` | TCP(-t) LISTEN(-l) 숫자(-n) PID(-p) |

---

## 문제 7 - RAID 비교 [recall]
> RAID 0, RAID 1, RAID 5를 비교하여 빈칸을 채우시오.
> | 구분 | RAID 0 | RAID 1 | RAID 5 |
> |------|--------|--------|--------|
> | 이름 | (가) | (나) | (다) |
> | 최소 디스크 | (라) | 2개 | (마) |
> | 장애 허용 | (바) | 1개 | 1개 |

> [!answer]- 정답 보기
> | 빈칸 | 정답 |
> |------|------|
> | (가) | **스트라이핑** (Striping) |
> | (나) | **미러링** (Mirroring) |
> | (다) | **스트라이핑 + 패리티** |
> | (라) | **2개** |
> | (마) | **3개** |
> | (바) | **불가** (복구 불가) |

---

## 문제 8 - LVM [application]
> LVM을 사용하여 `/dev/sdb1`과 `/dev/sdc1`을 묶어 20GB의 논리 볼륨 `lv_data`를 생성하는 과정을 명령어 순서대로 작성하시오. (볼륨 그룹 이름: `vg_storage`)

> [!answer]- 정답 보기
> ```bash
> # 1. PV (Physical Volume) 생성
> pvcreate /dev/sdb1 /dev/sdc1
>
> # 2. VG (Volume Group) 생성
> vgcreate vg_storage /dev/sdb1 /dev/sdc1
>
> # 3. LV (Logical Volume) 생성
> lvcreate -L 20G -n lv_data vg_storage
> ```
>
> LVM 순서: **PV → VG → LV** (`pvcreate` → `vgcreate` → `lvcreate`)
> 이후 `mkfs.ext4 /dev/vg_storage/lv_data`로 파일시스템 생성, `mount`로 마운트

---

## 문제 9 - 클러스터링 [recall]
> 다음 설명에 해당하는 클러스터 유형을 적으시오.
> (1) 베어울프(Beowulf) 클러스터로 대규모 연산을 수행
> (2) 로드밸런서를 사용하여 트래픽을 여러 서버에 분산
> (3) 장애 시 IP를 다른 서버로 자동 이전하여 서비스 연속성 보장

> [!answer]- 정답 보기
> | 번호 | 클러스터 유형 | 키워드 |
> |------|-------------|--------|
> | (1) | **HPC** (High Performance Computing) | 고성능 계산, 베어울프 |
> | (2) | **LVS** (Linux Virtual Server) | 부하 분산, 로드밸런서 |
> | (3) | **HA** (High Availability) | 고가용성, IP 이주(Failover) |

---

## 문제 10 - 가상화 [recall]
> 다음 설명에 해당하는 가상화 솔루션을 적으시오.
> (1) CPU 반가상화 방식의 가상화 솔루션
> (2) 레드햇 하이퍼바이저로, CPU 전가상화 방식
> (3) 컨테이너 기반 가상화 플랫폼

> [!answer]- 정답 보기
> | 번호 | 솔루션 | 특징 |
> |------|--------|------|
> | (1) | **Xen** | **반가상화**, 게스트 OS 수정 필요 |
> | (2) | **KVM** | **전가상화**, 레드햇, 커널 기반 |
> | (3) | **Docker** | **컨테이너** 기반, 경량, 이미지 배포 |
>
> VirtualBox는 오라클이 개발한 **독자적 가상 장치 관리자**로 데스크톱용 전가상화이다.

---

## 문제 11 - 클라우드 컴퓨팅 [analysis]
> 클라우드 컴퓨팅의 IaaS, PaaS, SaaS를 비교하고, 각각의 대표 서비스 예시를 한 가지씩 적으시오.

> [!answer]- 정답 보기
> | 모델 | 의미 | 제공 범위 | 대표 예시 |
> |------|------|-----------|-----------|
> | **IaaS** | Infrastructure as a Service | **하드웨어** 임대 | **Amazon EC2** |
> | **PaaS** | Platform as a Service | **개발 플랫폼** | **Google App Engine** |
> | **SaaS** | Software as a Service | **응용프로그램** | **Gmail**, 네이버 클라우드 |
>
> IaaS → PaaS → SaaS 순으로 사용자 관리 범위가 줄어들고, 클라우드 공급자 관리 범위가 늘어난다.

---

## 문제 12 - 종합 분석 [analysis]
> 다음 네트워크 관련 설정 파일과 그 역할을 연결하시오.
> (1) `/etc/hosts`
> (2) `/etc/resolv.conf`
> (3) `/etc/sysconfig/network`
>
> A. DNS 서버 주소 지정
> B. IP와 호스트명 직접 매핑
> C. 네트워크 기본 설정 (호스트명, 게이트웨이)

> [!answer]- 정답 보기
> | 파일 | 답 | 역할 |
> |------|-----|------|
> | (1) `/etc/hosts` | **B** | IP와 호스트명을 직접 매핑 (DNS 없이 로컬 해석) |
> | (2) `/etc/resolv.conf` | **A** | DNS 서버 주소 지정 (`nameserver 8.8.8.8`) |
> | (3) `/etc/sysconfig/network` | **C** | 호스트명, 게이트웨이 등 네트워크 기본 설정 (Red Hat 계열) |
>
> 이름 해석 순서: `/etc/hosts` → `/etc/resolv.conf`(DNS)

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | 키워드 | 정답 |
> |--------|------|
> | OSI 3계층 장비 | 라우터 |
> | OSI 2계층 장비 | 스위치/브릿지 |
> | 전송 계층 데이터 단위 | Segment |
> | IP → MAC | ARP |
> | MAC → IP | RARP |
> | 멀티캐스트 관리 | IGMP |
> | TCP 연결 설정 | SYN → SYN+ACK → ACK |
> | TCP 연결 해제 | FIN → ACK → FIN → ACK |
> | DNS 포트 | 53 |
> | SMTP/POP3 포트 | 25 / 110 |
> | ICMP 통신 점검 | ping |
> | 경로 추적 | traceroute |
> | netstat 대체 | ss |
> | ifconfig 대체 | ip |
> | RAID 0/1/5 | 스트라이핑/미러링/패리티 |
> | RAID 5 최소 디스크 | 3개 |
> | LVM 순서 | PV → VG → LV |
> | HPC 키워드 | 베어울프, 고성능 계산 |
> | LVS 키워드 | 로드밸런서, 부하 분산 |
> | HA 키워드 | IP 이주, 고가용성 |
> | Xen | 반가상화 |
> | KVM | 전가상화, 레드햇 |
> | Docker | 컨테이너 |
> | IaaS/PaaS/SaaS | 하드웨어/플랫폼/소프트웨어 |
> | DNS 설정 파일 | /etc/resolv.conf |
> | 호스트명 매핑 | /etc/hosts |
> | 하둡 | 대용량 분산처리, 자바 기반 |
