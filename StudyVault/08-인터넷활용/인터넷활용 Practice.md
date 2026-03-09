---
source_pdf: 원문 미보유 (웹 소스)
part: Part 3 Ch02
keywords: practice, network, raid, lvm, protocol
---

# 인터넷활용 Practice (10 questions)

#practice #network

## Related Concepts
- [[네트워크 기초]]
- [[네트워크 명령어와 서비스]]
- [[클러스터링과 스토리지]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | IP→MAC | ARP |
> | 3-way handshaking | TCP |
> | DNS 설정 파일 | /etc/resolv.conf |
> | RAID 5 최소 디스크 | 3개 |
> | LVM 순서 | PV→VG→LV |

---

## Question 1 - OSI 계층 [recall]
> TCP와 IP는 각각 OSI 몇 계층에 해당하는가?

> [!answer]- 정답 보기
> - **TCP**: 4계층 (전송 계층)
> - **IP**: 3계층 (네트워크 계층)

---

## Question 2 - 프로토콜 기능 [recall]
> ARP와 RARP의 역할을 각각 설명하시오.

> [!answer]- 정답 보기
> - **ARP**: IP 주소 → MAC 주소 변환 (주로 사용)
> - **RARP**: MAC 주소 → IP 주소 변환 (거의 사용 안 함)

---

## Question 3 - 포트 번호 [recall]
> SSH, HTTP, FTP(데이터), SMTP의 포트 번호는?

> [!answer]- 정답 보기
> - SSH: **22**, HTTP: **80**, FTP(데이터): **20**, SMTP: **25**
> - 참고: FTP 제어: 21, HTTPS: 443, DNS: 53

---

## Question 4 - RAID 비교 [recall]
> RAID 0, 1, 5의 최소 디스크 수와 방식을 각각 말하시오.

> [!answer]- 정답 보기
> | RAID | 최소 디스크 | 방식 |
> |------|-----------|------|
> | 0 | 2개 | 스트라이핑 |
> | 1 | 2개 | 미러링 |
> | 5 | **3개** | 패리티 분산 |

---

## Question 5 - LVM 순서 [recall]
> LVM에서 논리 볼륨을 생성하는 순서는?

> [!answer]- 정답 보기
> **PV(Physical Volume) → VG(Volume Group) → LV(Logical Volume)**
> `pvcreate` → `vgcreate` → `lvcreate`

---

## Question 6 - 클라우드 분류 [recall]
> IaaS, PaaS, SaaS를 추상화 수준이 낮은 순서부터 나열하시오.

> [!answer]- 정답 보기
> **IaaS → PaaS → SaaS** — IaaS(인프라) → PaaS(플랫폼) → SaaS(소프트웨어). SaaS가 가장 추상화 수준이 높음.

---

## Question 7 - 네트워크 명령어 [application]
> 서버에서 특정 포트로 서비스가 정상 동작하는지 확인하려면 어떤 명령어를 사용하는가?

> [!answer]- 정답 보기
> `netstat -tlnp` — TCP 리스닝 포트와 해당 프로세스를 확인
> 또는 `ss -tlnp` (최신 리눅스)

---

## Question 8 - DNS 설정 [application]
> DNS 서버를 8.8.8.8로 변경하려면 어떤 파일을 수정해야 하는가?

> [!answer]- 정답 보기
> `/etc/resolv.conf` — `nameserver 8.8.8.8` 추가/수정

---

## Question 9 - TCP vs UDP 적용 [analysis]
> 실시간 화상 회의 시스템에 TCP와 UDP 중 어떤 프로토콜이 적합한지 근거와 함께 설명하시오.

> [!answer]- 정답 보기
> **UDP**가 적합
> - 실시간 스트리밍은 **속도**가 중요하며 약간의 패킷 손실은 허용 가능
> - TCP의 재전송 메커니즘은 오히려 지연을 유발
> - 단, 신뢰성이 필요한 채팅/파일 전송은 TCP 병행

---

## Question 10 - RAID 선택 [analysis]
> 회사 DB 서버에 RAID를 구성하려 한다. RAID 0, 1, 5 중 가장 적합한 것을 선택하고 근거를 설명하시오.

> [!answer]- 정답 보기
> **RAID 5** 추천
> | 항목 | RAID 0 | RAID 1 | RAID 5 |
> |------|--------|--------|--------|
> | 데이터 보호 | ✗ | ✓ | ✓ |
> | 성능 | 최고 | 보통 | 좋음 |
> | 용량 효율 | 100% | 50% | (n-1)/n |
>
> DB 서버는 **데이터 안전성**과 **성능** 모두 필요. RAID 5는 패리티로 1개 디스크 장애 복구 가능하면서 용량 효율도 RAID 1보다 높음.

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | IP→MAC | ARP |
> | TCP 계층 | 4계층(전송) |
> | SSH 포트 | 22 |
> | DNS 설정 | /etc/resolv.conf |
> | RAID 5 최소 | 3개 디스크 |
> | LVM 순서 | PV→VG→LV |
> | IaaS 예시 | AWS EC2 |
