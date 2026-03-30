# Requirement SoT Management

Obsidian 기반 요구사항 Source of Truth(SoT) 관리 시스템입니다.
회의 → 요구사항 변경 → 결정사항 추적까지의 전체 흐름을 Obsidian + Claude로 관리합니다.

---

## 폴더 구조

```
SoT/
├── 00_Inbox          # 정리 전 메모, 아이디어
├── 01_Requirements   # 요구사항 문서 (RQ-XXX)
├── 02_Decisions      # 결정사항 문서 (DEC-XXX)
├── 03_Meetings       # 회의록 (날짜 기반)
├── 04_Glossary       # 용어 정의
├── 99_Templates      # 템플릿 (RQ, DEC, MEET)
└── Dashboard.md      # Dataview 대시보드
```

---

## 시작하기

### 1. Obsidian으로 열기

이 폴더를 Obsidian Vault로 열면 바로 사용할 수 있습니다.

### 2. 필수 커뮤니티 플러그인

| 플러그인 | 용도 |
|---------|------|
| **Templater** | 템플릿 날짜 자동 입력 |
| **QuickAdd** | 빠른 문서 생성 (번호/기능명 입력 → 파일 자동 생성) |
| **Dataview** | Dashboard 테이블 쿼리 |

> 설정 → 커뮤니티 플러그인 → 찾아보기에서 설치 후 활성화

---

## 사용 방법

### 요구사항 생성 (RQ)

1. `Ctrl/Cmd + P` → QuickAdd → **Creat Requirement** 선택
2. 번호(num)와 기능명(func) 입력
3. `RQ-001-로그인.md` 형태로 자동 생성

**규칙:**
- 바로 RQ를 만들지 말고 `00_Inbox`에 먼저 메모 → 정리 후 생성
- **사용자 행동/기능 단위**로 생성 (버튼 단위 X, 화면 단위 X)

### 결정사항 생성 (DEC)

1. `Ctrl/Cmd + P` → QuickAdd → **Creat Decision** 선택
2. 번호와 제목 입력
3. **논쟁이 있었던 항목만** 기록 (전부 기록하면 안 쓰게 됨)

### 회의록 생성 (MEET)

1. `Ctrl/Cmd + P` → QuickAdd → **Creat Meeting** 선택
2. 날짜 기반 파일 자동 생성

---

## 핵심 워크플로우

```
회의 발생 → MEET 작성 → Claude 분석 → RQ/DEC 생성·수정 → 링크 연결 → Dashboard 확인
```

### Step 1. 회의록 작성
QuickAdd로 Meeting 생성 후 내용 작성

### Step 2. Claude에 분석 요청
회의 내용을 Claude에 입력하고 요청:

> "변경된 요구사항 / 신규 요구사항 / Decision 필요 항목 정리해줘"

Claude가 아래 형식으로 분석:

```
[Changes]        - RQ-001: (변경 내용)
[New]            - RQ-XXX: (신규 요구사항)
[Decisions]      - DEC-XXX: (결정 필요 사유)
[Impact]         - RQ-001 → RQ-002, RQ-005 영향
```

### Step 3. 반영
- 기존 RQ 수정 (변경이력에 날짜/내용 기록)
- 신규 RQ, DEC 생성
- `[[RQ-001-로그인]]` 형태로 문서 간 링크 연결

### Step 4. 확인
- **Dashboard.md**: 전체 요구사항, 미결 결정사항, 최근 회의 조회
- **그래프뷰**: 문서 간 연결 관계 시각화
- **백링크**: 특정 RQ에 영향을 준 회의/결정 추적

---

## 문서 연결 체계

| 문서 | ID 형식 | 연결 대상 |
|------|---------|----------|
| Requirement | `RQ-001` | 관련 RQ, DEC, MEET |
| Decision | `DEC-001` | 관련 RQ, MEET |
| Meeting | `YYYY-MM-DD` | 관련 RQ, DEC |

Obsidian `[[위키링크]]`로 연결하면 양방향 추적이 가능합니다.

---

## 프론트매터 (Dataview용)

각 템플릿에 YAML 프론트매터가 포함되어 있어 Dataview 쿼리가 가능합니다.

**RQ**: `상태`, `담당자`, `생성일`, `수정일`, `카테고리`
**DEC**: `상태(open/closed)`, `생성일`, `관련RQ`
**MEET**: `날짜`, `참석자`

---

## 핵심 원칙

- **Obsidian = DB** / md 파일 = 레코드 / 링크 = 관계 / Claude = 분석 엔진
- RQ는 기능 단위, DEC은 논쟁 있었던 것만
- Claude는 제안만 하고, 반영은 사람(PM)이 직접 수행
