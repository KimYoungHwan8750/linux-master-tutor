---
name: tutor-setup
description: >
  Transforms knowledge sources into an Obsidian StudyVault. Two modes:
  (1) Document Mode — PDF/text/web sources → study notes with practice questions.
  (2) Codebase Mode — source code project → onboarding vault for new developers.
  Mode is auto-detected based on project markers in CWD.
argument-hint: "[source-path-or-url]"
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, WebFetch
---

# 튜터 셋업 — 지식 소스를 Obsidian StudyVault로 변환

## CWD 경계 규칙 (모든 모드 공통)

> **현재 작업 디렉토리(CWD) 외부의 파일에 절대 접근하지 않는다.**
> 모든 소스 스캔, 읽기, 볼트 출력은 CWD와 그 하위 디렉토리 내에서만 수행.
> 사용자가 외부 경로를 제공하면, CWD로 파일을 복사해달라고 안내.

## 모드 감지

실행 시 자동으로 모드 감지:

1. **프로젝트 마커 확인** (CWD):
   - `package.json`, `pom.xml`, `build.gradle`, `Cargo.toml`, `go.mod`, `Makefile`,
     `*.sln`, `pyproject.toml`, `setup.py`, `Gemfile`
2. **마커 발견 시** → **코드베이스 모드**
3. **마커 없을 시** → **문서 모드**
4. **판정 불가**: `.git/`만 존재하고 소스 코드 파일(`*.ts`, `*.py`, `*.java`, `*.go`, `*.rs` 등)이 없으면 문서 모드 기본.
5. 감지된 모드를 안내하고 사용자 확인/변경 요청.

---

## 문서 모드

> 지식 소스(PDF, 텍스트, 웹, epub)를 학습 노트로 변환.
> 템플릿: [templates.md](references/templates.md)

### Phase D1: 소스 발견 및 추출

1. **CWD 자동 스캔**: `**/*.pdf`, `**/*.txt`, `**/*.md`, `**/*.html`, `**/*.epub` (`node_modules/`, `.git/`, `dist/`, `build/`, `StudyVault/` 제외). 사용자에게 확인.
2. **텍스트 추출 (필수 도구)**:
   - **PDF → `pdftotext` CLI만 사용** (Bash 도구로 실행). Read 도구로 PDF를 직접 읽지 않는다 — 페이지를 이미지로 렌더링하여 10~50배 토큰 낭비. 먼저 `.txt`로 변환 후 읽기.
     ```bash
     pdftotext "source.pdf" "/tmp/source.txt"
     ```
   - `pdftotext` 미설치 시: `brew install poppler` (macOS) 또는 `apt-get install poppler-utils` (Linux).
   - URL → WebFetch
   - 기타 형식(`.md`, `.txt`, `.html`) → Read 직접 사용.
3. **변환된 `.txt` 파일 읽기** — 범위, 구조, 깊이 파악. 변환된 텍스트에서만 작업, 원본 PDF 사용 금지.
4. **소스 콘텐츠 매핑 (다중 파일 소스일 때 필수)**:
   - 모든 소스 파일의 **표지 + 목차 + 중간/끝에서 3+ 샘플 페이지** 읽기
   - **파일명에서 내용을 추측하지 않는다** — 파일 번호 ≠ 챕터 번호일 수 있음
   - 검증된 매핑 구축: `{ 소스파일 → 실제 주제 → 페이지 범위 }`
   - 비학술 파일, 누락 소스 표시
   - 매핑을 사용자에게 제시하여 검증 후 진행

### Phase D2: 콘텐츠 분석

1. 주제 계층 식별 — 섹션, 챕터, 도메인 구분.
2. 개념 콘텐츠 vs 연습 문제 분리.
3. 주제 간 의존성 매핑.
4. 핵심 패턴 식별 — 비교, 의사결정 트리, 공식.
5. **전체 주제 체크리스트 (필수)** — 모든 주제/소주제 나열. 이후 모든 단계의 기준.

> **균등 깊이 규칙**: 간략히 언급된 소주제라도 교과서 수준 지식을 보충한 **완전한 전용 노트**를 작성해야 한다.

6. **분류 완전성**: 소스에서 카테고리를 열거할 때("3가지 유형의 X"), 모든 멤버에 전용 노트 작성. 스캔 대상: "유형", "N가지", "종류", "types of", "categories", "there are N".
7. **소스-노트 교차 검증 (필수)**: 각 주제를 다루는 소스 파일과 페이지 범위 기록. 추적 불가 주제는 "소스 미보유"로 표시.

### Phase D3: 태그 표준

노트 작성 전 태그 어휘 정의:
- **형식**: 영문, 소문자, 케밥 케이스 (예: `#data-hazard`)
- **계층**: 최상위 → 도메인 → 세부 → 기법 → 노트유형
- **레지스트리**: 등록된 태그만 사용 가능. 세부 태그에 상위 도메인 태그 함께 부착.

### Phase D4: 볼트 구조

[templates.md](references/templates.md)에 따라 `StudyVault/`에 번호 폴더 생성. 관련 개념 3~5개를 파일 하나에 묶기.

### Phase D5: 대시보드 생성

`00-Dashboard/` 생성: MOC, 빠른 참조, 시험 함정. [templates.md](references/templates.md) 참조.

- **MOC**: 주제 맵 + 연습 노트 + 학습 도구 + 태그 인덱스(규칙 포함) + 취약 영역(링크 포함) + 비핵심 주제 정책
- **빠른 참조**: 모든 헤딩에 `→ [[개념 노트]]` 링크; 모든 핵심 공식
- **시험 함정**: 주제별 함정 포인트 (접기 콜아웃), 개념 노트 링크

### Phase D6: 개념 노트

[templates.md](references/templates.md)에 따라 작성. 핵심 규칙:
- YAML frontmatter: `source_pdf`, `part`, `keywords` (필수)
- **source_pdf는 Phase D1에서 검증한 매핑과 반드시 일치** — 파일명에서 추측 금지
- 미보유 시: `source_pdf: 원문 미보유`
- `[[wiki-links]]`, 콜아웃(`[!tip]`, `[!important]`, `[!warning]`), 비교표 > 산문
- 프로세스/흐름/순서에 ASCII 다이어그램
- **단순화-예외 규칙**: 일반 서술에 반드시 예외 사항 명시

### Phase D7: 연습 문제

[templates.md](references/templates.md)에 따라 작성. 핵심 규칙:
- 모든 주제 폴더에 연습 파일 필수 (8문제 이상)
- **능동적 회상**: 답안은 `> [!answer]- 정답 보기` 접기 콜아웃
- 패턴은 `> [!hint]-` / `> [!summary]-` 접기 콜아웃
- **문제 유형 다양성**: ≥60% 기억, ≥20% 응용, ≥2 분석 (파일당)
- `## 관련 개념`에 `[[wiki-links]]`

### Phase D8: 상호 링크

1. 모든 개념 노트에 `## 관련 노트`
2. MOC에서 모든 개념 + 연습 노트 링크
3. 개념 ↔ 연습 교차 링크; 형제 노트 상호 참조
4. 빠른 참조 섹션 → `[[개념 노트]]` 링크
5. 취약 영역 → 관련 노트 + 시험 함정; 시험 함정 → 개념 노트

### Phase D9: 자체 검토 (필수)

[quality-checklist.md](references/quality-checklist.md) **문서 모드** 섹션 기준으로 검증. 모든 항목 통과할 때까지 수정 및 재검증.

---

## 코드베이스 모드

> 소스 코드 프로젝트에서 신규 개발자 온보딩 StudyVault 생성.
> 전체 워크플로우: [codebase-workflow.md](references/codebase-workflow.md)
> 템플릿: [codebase-templates.md](references/codebase-templates.md)

### 단계 요약

| 단계 | 이름 | 핵심 작업 |
|------|------|-----------|
| C1 | 프로젝트 탐색 | 파일 스캔, 기술 스택 감지, 엔트리 포인트 읽기, 디렉토리 레이아웃 매핑 |
| C2 | 아키텍처 분석 | 패턴 식별, 요청 흐름 추적, 모듈 경계·데이터 흐름 매핑 |
| C3 | 태그 표준 | `#arch-*`, `#module-*`, `#pattern-*`, `#api-*` 태그 레지스트리 정의 |
| C4 | 볼트 구조 | `StudyVault/` 생성: Dashboard, Architecture, 모듈별, DevOps, Exercises 폴더 |
| C5 | 대시보드 | MOC (모듈 맵 + API 서피스 + 시작 가이드 + 온보딩 경로) + 빠른 참조 |
| C6 | 모듈 노트 | 모듈별 노트: 목적, 핵심 파일, 공개 인터페이스, 내부 흐름, 의존성 |
| C7 | 온보딩 연습 | 코드 읽기, 설정, 디버깅, 확장 연습 (주요 모듈당 5개 이상) |
| C8 | 상호 링크 | 모듈 간 교차 링크, 아키텍처 ↔ 구현, 연습 ↔ 모듈 |
| C9 | 자체 검토 | [quality-checklist.md](references/quality-checklist.md) **코드베이스 모드** 기준 검증 |

상세 단계별 지침: [codebase-workflow.md](references/codebase-workflow.md) 참조.

---

## 언어

- 소스 자료 언어에 맞춤 (한국어 자료 → 한국어 노트 등)
- **태그/키워드**: 항상 영문
