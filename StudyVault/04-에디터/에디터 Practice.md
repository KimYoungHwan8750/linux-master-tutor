---
source_pdf: 원문 미보유 (웹 소스)
part: Part 2 Ch04
keywords: practice, vi, editor, vim
---

# 에디터 Practice (8 questions)

#practice #editor

## Related Concepts
- [[에디터]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | 저장 후 종료 | :wq |
> | 강제 종료 | :q! |
> | 전체 치환 | :%s/old/new/g |
> | 줄 삭제 | dd |
> | 입력모드 진입 | i, a, o |

---

## Question 1 - vi 모드 [recall]
> vi 에디터의 3가지 모드를 나열하시오.

> [!answer]- 정답 보기
> **명령모드(command mode)**, **입력모드(insert mode)**, **라인모드(ex mode/last line mode)**

---

## Question 2 - 입력모드 진입 [recall]
> vi에서 커서 위치 다음 줄에 새 줄을 삽입하며 입력모드로 전환하는 키는?

> [!answer]- 정답 보기
> **o** — 현재 줄 아래에 새 줄 삽입 후 입력모드 진입. O는 위 줄에 삽입.

---

## Question 3 - 저장/종료 명령 [recall]
> vi에서 변경 사항을 저장하지 않고 강제 종료하는 명령은?

> [!answer]- 정답 보기
> **:q!** — 라인모드에서 q!로 저장 없이 강제 종료

---

## Question 4 - 검색과 치환 [recall]
> vi에서 파일 전체의 "linux"를 "LINUX"로 모두 변경하는 명령은?

> [!answer]- 정답 보기
> `:%s/linux/LINUX/g` — %는 전체 파일, s는 치환, g는 줄 내 모든 일치 항목

---

## Question 5 - 편집 명령 [recall]
> vi 명령모드에서 현재 줄을 복사한 후 아래에 붙여넣기하는 키 조합은?

> [!answer]- 정답 보기
> **yy** (줄 복사) → **p** (아래에 붙여넣기)

---

## Question 6 - 다른 에디터 비교 [recall]
> emacs에서 파일을 저장하는 단축키는?

> [!answer]- 정답 보기
> **Ctrl+x Ctrl+s** — emacs는 모드 구분 없이 Ctrl 키 조합 사용

---

## Question 7 - vi 실무 활용 [application]
> 설정 파일에서 모든 "192.168.1.1"을 "10.0.0.1"로 변경해야 한다. vi에서 가장 효율적인 방법은?

> [!answer]- 정답 보기
> `:%s/192.168.1.1/10.0.0.1/g` — 전체 파일에서 일괄 치환. 확인하며 변경하려면 끝에 `c` 추가: `:%s/192.168.1.1/10.0.0.1/gc`

---

## Question 8 - vi vs emacs vs nano 비교 [analysis]
> vi, emacs, nano 에디터의 장단점을 비교하고, 각각 어떤 상황에 적합한지 설명하시오.

> [!answer]- 정답 보기
> | 항목 | vi/vim | emacs | nano |
> |------|--------|-------|------|
> | 학습 곡선 | 높음 | 중간 | 낮음 |
> | 모드 | 3가지 모드 | 단일 모드 | 단일 모드 |
> | 확장성 | 플러그인 | Lisp 확장 | 제한적 |
> | 적합 상황 | 서버 관리, 고급 편집 | 개발, 다기능 | 간단한 편집, 초보자 |
>
> 대부분의 리눅스 시스템에 vi는 기본 설치되어 있으므로 반드시 학습 필요.

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | Keyword | Answer |
> |---------|--------|
> | 저장 후 종료 | :wq |
> | 저장 안하고 종료 | :q! |
> | 줄 삭제 | dd |
> | 줄 복사 | yy |
> | 전체 치환 | :%s/old/new/g |
> | 아래 줄 삽입 | o |
