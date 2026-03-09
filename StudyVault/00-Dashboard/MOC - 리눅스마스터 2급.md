---
source_pdf: 원문 미보유 (웹 소스)
part: all
keywords: MOC, study map, linux-master
---

# 리눅스마스터 2급 2차 Study Map

#dashboard #linux-master

## Overview
- **시험명**: 리눅스마스터 2급 2차
- **출제 범위**: Part 2 (리눅스 운영 및 관리) + Part 3 (리눅스 활용)
- **전략**: 개념 정리 + 3개년 기출 풀이로 합격 가능

## Topic Map
| Section | Source | Notes | Status |
|---------|--------|-------|--------|
| 파일 시스템 명령어 | Part 2 Ch01 | [[파일 권한과 소유권]], [[디스크 쿼타와 파일시스템]], [[파일시스템 관리 명령어]] | [ ] |
| 셸(Shell) | Part 2 Ch02 | [[셸의 종류와 특징]], [[셸 환경설정]] | [ ] |
| 프로세스 관리 | Part 2 Ch03 | [[프로세스 관리]] | [ ] |
| 에디터 | Part 2 Ch04 | [[에디터]] | [ ] |
| 소프트웨어 설치 및 삭제 | Part 2 Ch05 | [[소프트웨어 설치 및 삭제]] | [ ] |
| 장치 설정 | Part 2 Ch06 | [[장치 설정]] | [ ] |
| X-Windows | Part 3 Ch01 | [[X-Windows]] | [ ] |
| 인터넷 활용 | Part 3 Ch02 | [[네트워크 기초]], [[네트워크 명령어와 서비스]], [[클러스터링과 스토리지]] | [ ] |

## Practice Notes
| 문제셋 | 문항 수 | 링크 |
|--------|---------|------|
| 파일시스템 | 10문제 | [[파일시스템 Practice]] |
| 셸 | 10문제 | [[셸 Practice]] |
| 프로세스 관리 | 10문제 | [[프로세스관리 Practice]] |
| 에디터 | 8문제 | [[에디터 Practice]] |
| 소프트웨어 설치 | 8문제 | [[소프트웨어설치 Practice]] |
| 장치 설정 | 8문제 | [[장치설정 Practice]] |
| X-Windows | 8문제 | [[X-Windows Practice]] |
| 인터넷 활용 | 10문제 | [[인터넷활용 Practice]] |

## Study Tools
| 도구 | 설명 | 링크 |
|------|------|------|
| Exam Traps | 시험 함정/오답 포인트 모음 | [[Exam Traps]] |
| Quick Reference | 전체 치트시트 | [[빠른 참조]] |

## Tag Index
| Tag | 관련 주제 | 규칙 |
|-----|-----------|------|
| `#linux-master` | 리눅스마스터 전체 | 최상위 태그 |
| `#filesystem` | 파일 시스템, 마운트, 디스크 | 도메인 태그 |
| `#permission` | 허가권, SetUID, SetGID, Sticky bit | `#filesystem` 하위 |
| `#quota` | 디스크 쿼타 | `#filesystem` 하위 |
| `#shell` | 셸 종류, 환경설정 | 도메인 태그 |
| `#process` | 프로세스, 데몬 | 도메인 태그 |
| `#editor` | vi, emacs, nano | 도메인 태그 |
| `#package` | RPM, YUM, APT, 소스 설치 | 도메인 태그 |
| `#device` | 프린터, 사운드, 스캐너 | 도메인 태그 |
| `#x-windows` | X서버, 데스크톱 환경 | 도메인 태그 |
| `#network` | 네트워크, OSI, TCP/IP | 도메인 태그 |
| `#protocol` | HTTP, FTP, SMTP 등 프로토콜 | `#network` 하위 |
| `#storage` | RAID, LVM, 클러스터링 | `#network` 하위 |
| `#dashboard` | 대시보드 노트 | 노트 유형 태그 |
| `#exam-traps` | 시험 함정 포인트 | 노트 유형 태그 |
| `#practice` | 연습 문제 | 노트 유형 태그 |

> **태그 규칙**: 모든 태그는 영어 소문자 kebab-case. 세부 태그 사용 시 반드시 상위 도메인 태그도 함께 부착.

## Weak Areas
- [ ] SetUID/SetGID/Sticky bit 구분 → [[파일 권한과 소유권]] → [[Exam Traps]]
- [ ] OSI 7계층 프로토콜 매핑 → [[네트워크 기초]] → [[Exam Traps]]
- [ ] vi 명령모드 vs 입력모드 키 구분 → [[에디터]] → [[Exam Traps]]
- [ ] RPM vs YUM 옵션 차이 → [[소프트웨어 설치 및 삭제]] → [[Exam Traps]]
- [ ] RAID 레벨별 특성 → [[클러스터링과 스토리지]] → [[Exam Traps]]

## Non-core Topic Policy
| Source | Content | Handling |
|--------|---------|----------|
| 웹 소스 | 시험 전략/합격 후기 | **Excluded** — 학습 내용과 무관 |
