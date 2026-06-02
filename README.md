# 요구사항 SSOT 관리 시스템

Obsidian 기반 소프트웨어 기획·개발 프로세스의 요구사항 단일 진실 공급원(Single Source of Truth)을 관리합니다.  
도메인 배경 → 운영 정책 → 요구사항 → 기능 → 구현 명세까지 하나의 흐름으로 연결됩니다.

---

## 설계 컨셉

### 핵심 3계층 구조

```
RQ (WHY)  →  FT (WHAT)  →  SP (HOW + 구현상태)
                 ↑
              POL 참조
```

| 레이어     | 질문          | 폴더                     | 역할           |
| ------- | ----------- | ---------------------- | ------------ |
| **RQ**  | 왜 만드는가      | `07_Requirements/`     | 비즈니스 목적      |
| **FT**  | 무엇을 만드는가    | `09_Features/`         | 기능 정의        |
| **SP**  | 어떻게 만드는가    | `10_Specs/`            | 구현 명세 + 백로그  |
| **POL** | 어떤 규칙을 따르는가 | `04_Structure/Policy/` | 확정된 운영 정책    |

### 배경 레이어 → 산출 레이어

```
01~04 (배경: 프로젝트·용어·도메인·구조)
        ↓
05~06 (활동: 회의 발생 → 결정 기록)
        ↓
07~10 (산출: RQ → FT → SP 계층 관리)
```

- RQ는 Context와 Structure 위에서 해석. 배경 없는 요구사항은 작성 금지.
- Decision은 검토 과정의 기록, Policy는 그 결과로 확정된 약속.

---

## 폴더 구조

```
SoT/
├── 00_Dashboard.md            # Dataview 기반 전체 현황 대시보드
│
├── 01_Project/                # 프로젝트 헌장, 이해관계자
├── 02_Glossary/               # 도메인 용어집, 기준값 마스터 (업무구분·기능유형)
│
├── 03_Context/                # 도메인 배경지식
│   ├── Cycle.md               # 전체 운영 사이클 (주체의 시스템 생애주기, 프로젝트당 1개)
│   └── DDD/                   # 도메인 주도 설계 분석 (이벤트스토밍 등)
│
├── 04_Structure/              # 시스템 구조 + 운영 정책
│   ├── Policy/                # 확정된 운영 정책 (POL-XXX)
│   ├── User/                  # 사용자 유형, 역할 정의 (ROLE-XXX)
│   ├── Menu/                  # 메뉴 구조
│   └── Data/                  # 데이터 정의서 (DATA-XXX)
│
├── 05_Meetings/               # 회의록 (YYYY-MM-DD.md)
├── 06_Decisions/              # 의사결정 이력 (DEC-XXX)
│
├── 07_Requirements/           # 비즈니스 요구사항 (RQ-XXX)
├── 08_Diagrams/               # 다이어그램
│   ├── BPMN/
│   ├── UserFlow/
│   ├── Flowchart/
│   ├── Sequence/
│   └── Wireframe/
│
├── 09_Features/               # 기능 정의 (FT-XXX)
├── 10_Specs/                  # 구현 명세 + 백로그 (SP-XXX)
│
├── 11_AdminGuide/             # 운영자 가이드 (00_개요 ~ 10_FAQ)
└── 99_Templates/              # 문서 템플릿 11종 (RQ·FT·SP·POL·DEC 등)
```

---

## 시작하기

### 1단계: 기준값 정의

`SoT/02_Glossary/카테고리_목록.md`를 열어 프로젝트에 맞는 **업무구분**과 담당자를 정의합니다.  
기능유형은 범용 UX 패턴이므로 대부분 그대로 사용 가능합니다.

### 2단계: 문서 체계 초기화

```
01_Project 작성  (프로젝트 헌장, 이해관계자)
→ 02_Glossary 용어·기준값 확정
→ 03_Context/Cycle.md  (전체 운영 사이클)
→ 03_Context/DDD/  (도메인 분석)
→ 04_Structure  (Policy / User / Menu / Data)
→ 07_Requirements  (RQ)
→ 09_Features  (FT, 부모RQ 연결)
→ 10_Specs  (SP, 부모FT·부모RQ 연결)
```

### 3단계: 지속 관리

```
회의 발생 → 05_Meetings 작성
→ 변경된 FT·SP 구현상태 업데이트
→ 신규 SP 필요 시 현재 최대 번호 + 1로 생성
→ 정책 변경 시 04_Structure/Policy/POL-XXX 수정
→ 주요 결정 시 06_Decisions/DEC-XXX 생성
```

---

## 대시보드 (`SoT/00_Dashboard.md`)

Dataview 쿼리 기반 동적 현황판. Obsidian에서만 렌더링됩니다.

| 섹션 | 내용 |
|---|---|
| **SP 파이프라인** | 기획 / 퍼블 / 개발 / 완료 / 검증완료 단계별 개수 |
| **단계별 상세** | 부모FT · 업무구분 · 우선순위 · 담당자 |
| **RQ→FT→SP 연관** | 업무구분별 전체 연결 현황 |
| **FT 진행 현황** | 부모RQ · 기능유형 · 상태 · 담당자 |
| **RQ 달성 현황** | 업무구분 · 상태 |
| **미결 결정사항** | 상태=open인 DEC 목록 |
| **최근 회의** | 최근 5건 |

---

## 문서 ID 체계

| 유형 | ID 형식 | 위치 |
|---|---|---|
| 비즈니스 요구사항 | `RQ-XXX` | `07_Requirements/` |
| 기능 정의 | `FT-XXX` | `09_Features/` |
| 구현 명세 | `SP-XXX` | `10_Specs/` |
| 운영 정책 | `POL-XXX` | `04_Structure/Policy/` |
| 의사결정 | `DEC-XXX` | `06_Decisions/` |
| 데이터 정의 | `DATA-XXX` | `04_Structure/Data/` |
| 사용자 역할 | `ROLE-XXX` | `04_Structure/User/` |
| 다이어그램 | `BPMN/UF/FC/SEQ/WF-XXX` | `08_Diagrams/` |
| 회의록 | `YYYY-MM-DD` | `05_Meetings/` |

---

## 프론트매터 필드 규칙

### RQ
```yaml
유형: RQ
업무구분: # 02_Glossary/카테고리_목록.md 참조
상태: draft / confirmed / deprecated
```

### FT
```yaml
유형: FT
부모RQ: RQ-XXX
업무구분:
기능유형: # 02_Glossary/카테고리_목록.md 참조
상태: 설계중 / 개발중 / 완료
```

### SP
```yaml
유형: SP
부모FT: FT-XXX
부모RQ: RQ-XXX
업무구분:
기능유형:
구현상태: 기획 / 퍼블 / 개발 / 완료 / 검증완료
우선순위: P1 / P2 / P3
담당자:
출처: 기획설계 / 테스트조치 / 개발이슈 / 신규
```

### POL
```yaml
유형: POL
업무구분:
관련RQ: # RQ-XXX
관련DEC: # DEC-XXX
```

---

## 문서 연결 체계

```
03_Context/Cycle.md ──────────────→ 07_Requirements (사이클 단계 연결)
03_Context/DDD/ ───────────────────→ 07_Requirements (도메인 분석 → 요구사항)
04_Structure/Policy (POL-XXX) ─────→ 09_Features    (정책 참조)
04_Structure/User   (ROLE-XXX) ────→ 07_Requirements (역할 참조)
04_Structure/Data   (DATA-XXX) ────→ 10_Specs        (엔티티 참조)
07_Requirements (RQ) ──────────────→ 09_Features (FT)
09_Features     (FT) ──────────────→ 10_Specs    (SP)
06_Decisions (DEC) ────────────────→ 04_Structure/Policy (결정 근거 링크)
05_Meetings ───────────────────────→ 06_Decisions / 09_Features / 10_Specs
08_Diagrams ───────────────────────→ (참조용, 흐름의 중심 아님)
```

Obsidian `[[위키링크]]` 연결 시 양방향 추적 가능합니다.

---

## 운영 원칙

- **RQ는 현재 기준만 유지** — 과거 내용은 변경이력으로
- **FT 없는 SP 생성 금지** — 부모FT와 부모RQ는 필수 입력
- **SP 구현상태는 5단계만** — 기획 → 퍼블 → 개발 → 완료 → 검증완료 (`미완료` 없음)
- **Cycle.md는 프로젝트당 하나** — 주체의 전체 생애주기를 정의하는 단독 문서
- **POL은 DEC와 짝으로 관리** — 정책 변경 시 Decision을 병행 생성해 근거를 추적
- **Diagram은 설명 수단** — 산출물의 중심이 아닌 참조용

---

## 필수 플러그인 (Obsidian)

| 플러그인 | 용도 |
|---|---|
| **Dataview** | 대시보드 쿼리 (`00_Dashboard.md`) |
| **Templater** | 템플릿 날짜 자동 입력 |
| **QuickAdd** | 빠른 문서 생성 |
