# Requirement SoT Management

Obsidian 기반 프로젝트 관리 시스템입니다.
도메인 배경(Context) · 구조와 정책(Structure) · 요구사항(Requirements) · 의사결정 히스토리(Decisions)를 하나의 흐름으로 연결해 관리합니다.

---

## 설계 컨셉

```
프로젝트 전반 및 구조          검토사항            최종 산출물
─────────────────────        ──────────────      ──────────────
Project / Glossary           Meetings            Requirements
Context / Structure          Decisions           Diagrams
```

**핵심 원칙:**
- RQ는 Context와 Structure 위에서 해석된다. 배경 없는 요구사항은 작성하지 않는다.
- Decision은 검토 과정의 기록, Policy는 그 결과로 확정된 약속이다.

---

## 폴더 구조

```
SoT/
├── 00_Dashboard.md           # 전체 현황 대시보드
│
├── 01_Project                # 프로젝트 목표 / 범위 / 이해관계자 / RACI
├── 02_Glossary               # 도메인 용어 정의
│
├── 03_Context                # 도메인 지식 + 현황 분석
│   ├── Cycle.md              # 전체 운영 사이클 (주체의 시스템 생애주기, 단독)
│   └── {업무영역}/            # 예: Partner, Contract, 인수인계
│       └── Context.md        # 업무 분석 테이블 + 문제 정의
│
├── 04_Structure              # 시스템 구조 + 운영 규칙
│   ├── IA/                   # 정보구조
│   ├── Menu/                 # 메뉴 구조
│   ├── User/                 # UserTypes.md + ROLE-XXX (역할별 권한)
│   ├── Policy/               # 확정된 운영 약속
│   │   ├── AccountPolicy.md  # 계정 생성·수정·삭제 정책
│   │   ├── AccessControl.md  # 권한 부여·변경·회수 정책
│   │   └── OperationPolicy.md# 운영 약속 모음
│   └── Data/                 # 데이터 정의서 (DATA-XXX)
│
├── 05_Meetings               # 회의록 (YYYY-MM-DD)
├── 06_Decisions              # 검토·논의 이력 (DEC-XXX)
│
├── 07_Requirements           # 요구사항 SSOT (RQ-XXX)
├── 08_Diagrams               # 다이어그램 참조
│   ├── BPMN/
│   ├── UserFlow/
│   ├── Flowchart/
│   ├── Sequence/
│   └── Wireframe/            # 화면설계서 링크
│
├── 98_Memo                   # 임시 메모
└── 99_Templates              # 문서 템플릿
```

---

## 문서 역할 구분

| 문서                           | 역할                   | 성격     |
| ---------------------------- | -------------------- | ------ |
| `03_Context/Cycle.md`        | 주체의 시스템 생애주기 전체 흐름   | 도메인 지식 |
| `03_Context/{영역}/Context.md` | 업무 단위 분해 + 문제 정의     | 배경 분석  |
| `04_Structure/Policy/`       | 확정된 운영 약속 (현재 기준)    | 규칙     |
| `06_Decisions/`              | 검토·논의 이력 (왜 그렇게 됐는지) | 히스토리   |
| `07_Requirements/`           | 구현 기준 (현재 기준)        | 실행     |

---

## 문서 유형 및 ID 체계

| 문서 | ID 형식 | 위치 |
|------|---------|------|
| 요구사항 | `RQ-XXX` | 07_Requirements |
| 의사결정 | `DEC-XXX` | 06_Decisions |
| 회의록 | `YYYY-MM-DD` | 05_Meetings |
| 데이터 정의 | `DATA-XXX` | 04_Structure/Data |
| 사용자 역할 | `ROLE-XXX` | 04_Structure/User |
| 다이어그램 | `BPMN/UF/FC/SEQ/WF-XXX` | 08_Diagrams |

---

## 필수 플러그인 (Obsidian)

| 플러그인 | 용도 |
|---------|------|
| **Templater** | 템플릿 날짜 자동 입력 |
| **QuickAdd** | 빠른 문서 생성 |
| **Dataview** | Dashboard 쿼리 |

---

## 핵심 워크플로우

### 신규 프로젝트 시작

```
01_Project 작성
→ 02_Glossary 초안
→ 03_Context/Cycle.md (전체 운영 사이클)
→ 03_Context/{영역}/Context.md (업무 분석 + 문제 정의)
→ 04_Structure (IA / Menu / User / Policy / Data)
→ 07_Requirements
```

### 회의 발생 시

```
05_Meetings 작성 → Claude 분석 요청 → RQ / DEC 생성·수정 → Policy 업데이트 → 링크 연결
```

**Claude 분석 요청 예시:**
> "이 회의록 기반으로 변경된 RQ / 신규 RQ / Decision 필요 항목 / Policy 업데이트 사항 정리해줘"

Claude 분석 출력 형식:
```
[Changes]        RQ-001: (변경 내용)
[New]            RQ-XXX: (신규 요구사항)
[Decisions]      DEC-XXX: (검토 필요 사유)
[Policy Update]  04_Structure/Policy/{파일}: (확정된 약속 변경)
[Context Update] 03_Context/{영역}/Context.md: (업무 분석 변경)
[Impact]         RQ-001 → RQ-002, RQ-005 영향
```

---

## 문서 연결 체계

```
03_Context/Cycle.md ──────────────→ 07_Requirements (사이클 단계 연결)
03_Context/{영역}/Context.md ──────→ 07_Requirements (문제 → 요구사항)
04_Structure/Data ─────────────────→ 07_Requirements (엔티티 참조)
04_Structure/User ─────────────────→ 07_Requirements (역할 참조)
04_Structure/Policy ───────────────→ 07_Requirements (정책 참조)
                    ←── 06_Decisions (검토 이력 링크)
                    ←── 05_Meetings  (회의 링크)
08_Diagrams ───────────────────────→ (참조용, 중심 아님)
```

Obsidian `[[위키링크]]`로 연결 시 양방향 추적 가능.

---

## 운영 원칙

- **RQ는 항상 현재 기준만 유지** — 과거 내용은 변경이력으로
- **Cycle.md는 프로젝트당 하나** — 주체의 전체 생애주기를 정의
- **Context는 업무영역별로 분리** — RQ 작성 전 반드시 존재해야 함
- **Decision은 검토 과정** — Policy는 확정된 결과, 두 가지를 혼동하지 않는다
- **Policy는 Decision/Meeting을 링크** — 왜 그렇게 됐는지 항상 추적 가능하게
- **Diagram은 설명 수단** — 중심이 아닌 참조용
- **Claude는 제안만, 반영은 사람(PM)이 직접**
