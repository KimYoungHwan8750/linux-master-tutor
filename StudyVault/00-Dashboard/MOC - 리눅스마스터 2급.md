---
source_pdf: programjy.tistory.com
part: all
keywords: MOC, study map, linux-master-2
---

# 리눅스마스터 2급 학습 맵

#dashboard #linux-master

## 개요
- **시험명**: 리눅스마스터 2급 2차
- **범위**: Part 2 (리눅스 운영 및 관리) + Part 3 (리눅스 활용)
- **유형**: 실기 (80문항, CBT)
- **합격기준**: 60점 이상

## 주제 맵

| 섹션 | 소스 | 노트 | 상태 |
|------|------|------|------|
| 파일시스템 | Part2 Ch01 | [[파일 권한과 소유권]], [[디스크 쿼타와 파일시스템]], [[파일시스템 관리 명령어]] | [ ] |
| 셸 | Part2 Ch02 | [[셸의 종류와 특징]], [[셸 환경설정]] | [ ] |
| 프로세스 관리 | Part2 Ch03 | [[프로세스 관리]] | [ ] |
| 에디터 | Part2 Ch04 | [[에디터]] | [ ] |
| 소프트웨어 설치 | Part2 Ch05 | [[소프트웨어 설치 및 삭제]] | [ ] |
| 장치 설정 | Part2 Ch06 | [[장치 설정]] | [ ] |
| X-Windows | Part3 Ch01 | [[X-Windows]] | [ ] |
| 인터넷 활용 | Part3 Ch02 | [[네트워크 기초]], [[네트워크 명령어와 서비스]], [[클러스터링과 스토리지]] | [ ] |

## 연습 노트

| 문제셋 | 영역 | 링크 |
|--------|------|------|
| 파일시스템 | 권한, 쿼터, 마운트, 파일시스템 | [[파일시스템 Practice]] |
| 셸 | 셸 종류, 환경변수, 설정파일 | [[셸 Practice]] |
| 프로세스관리 | 프로세스, 시그널, 데몬, cron | [[프로세스관리 Practice]] |
| 에디터 | vi/vim, emacs, nano, crontab | [[에디터 Practice]] |
| 소프트웨어설치 | rpm, dpkg, yum, apt-get, 압축 | [[소프트웨어설치 Practice]] |
| 장치설정 | 프린터, 사운드, 스캐너 | [[장치설정 Practice]] |
| X-Windows | 데스크톱환경, 디스플레이매니저, xhost/xauth | [[X-Windows Practice]] |
| 인터넷활용 | 네트워크, OSI, TCP/UDP, RAID, LVM | [[인터넷활용 Practice]] |

## 학습 도구

| 도구 | 설명 | 링크 |
|------|------|------|
| 시험 함정 | 자주 틀리는 포인트 모음 | [[Exam Traps]] |
| 빠른 참조 | 전체 치트시트 | [[빠른 참조]] |

## 태그 인덱스

| 태그 | 관련 주제 | 규칙 |
|------|-----------|------|
| `#linux-master` | 전체 | 최상위 |
| `#filesystem` | 파일시스템 | 도메인 |
| `#shell` | 셸 | 도메인 |
| `#process` | 프로세스 | 도메인 |
| `#editor` | 에디터 | 도메인 |
| `#package-mgmt` | 소프트웨어 설치 | 도메인 |
| `#device` | 장치 설정 | 도메인 |
| `#x-windows` | X-Windows | 도메인 |
| `#network` | 네트워크/인터넷 | 도메인 |
| `#permission` | 파일 권한 | 세부 (+filesystem) |
| `#disk-quota` | 디스크 쿼터 | 세부 (+filesystem) |
| `#mount` | 마운트/관리 | 세부 (+filesystem) |
| `#fs-type` | 파일시스템 유형 | 세부 (+filesystem) |
| `#env-var` | 환경변수 | 세부 (+shell) |
| `#config-file` | 설정파일 | 세부 (+shell) |
| `#daemon` | 데몬 | 세부 (+process) |
| `#signal` | 시그널 | 세부 (+process) |
| `#scheduling` | 스케줄링 | 세부 (+process) |
| `#vi-vim` | vi/vim | 세부 (+editor) |
| `#crontab` | 크론탭 | 세부 (+editor) |
| `#rpm-dpkg` | RPM/DPKG | 세부 (+package-mgmt) |
| `#compression` | 압축 | 세부 (+package-mgmt) |
| `#source-install` | 소스 설치 | 세부 (+package-mgmt) |
| `#printer` | 프린터 | 세부 (+device) |
| `#sound` | 사운드 | 세부 (+device) |
| `#scanner` | 스캐너 | 세부 (+device) |
| `#desktop-env` | 데스크톱 환경 | 세부 (+x-windows) |
| `#display-mgr` | 디스플레이 매니저 | 세부 (+x-windows) |
| `#window-mgr` | 윈도우 매니저 | 세부 (+x-windows) |
| `#osi-model` | OSI 모델 | 세부 (+network) |
| `#tcp-udp` | TCP/UDP | 세부 (+network) |
| `#network-cmd` | 네트워크 명령어 | 세부 (+network) |
| `#internet-svc` | 인터넷 서비스 | 세부 (+network) |
| `#raid` | RAID | 세부 (+network) |
| `#lvm` | LVM | 세부 (+network) |
| `#cluster` | 클러스터링 | 세부 (+network) |
| `#virtualization` | 가상화 | 세부 (+network) |
| `#cloud` | 클라우드 | 세부 (+network) |
| `#practice` | 연습 문제 | 유형 |
| `#dashboard` | 대시보드 | 유형 |
| `#exam-traps` | 시험 함정 | 유형 |

> **태그 규칙**: 영문 케밥 케이스만 사용. 세부 태그는 반드시 상위 도메인 태그와 함께 부착.

## 취약 영역
- [ ] 파악 필요 → 학습 후 업데이트
- [ ] 취약 영역 → [[관련 노트]] → [[Exam Traps]]

## 비핵심 주제 정책

| 소스 | 내용 | 처리 |
|------|------|------|
| 해당 없음 | 모든 내용 포함 | 전체 포함 |
