# Dashboard

## 단계별 SP 현황 (파이프라인)

```dataview
table length(rows) as "개수"
from "SoT/10_Specs"
group by 구현상태
```

---

## 기획 단계

```dataview
table 부모FT, 업무구분, 우선순위, 담당자
from "SoT/10_Specs"
where 구현상태 = "기획"
sort 우선순위 asc, 업무구분 asc
```

## 퍼블 단계

```dataview
table 부모FT, 업무구분, 담당자
from "SoT/10_Specs"
where 구현상태 = "퍼블"
sort 우선순위 asc
```

## 개발 단계

```dataview
table 부모FT, 업무구분, 우선순위, 담당자
from "SoT/10_Specs"
where 구현상태 = "개발"
sort 우선순위 asc, 업무구분 asc
```

---

## RQ → FT → SP 연관 현황

```dataview
table rows.부모RQ, rows.부모FT, rows.구현상태, rows.우선순위
from "SoT/10_Specs"
group by 업무구분
```

---

## FT 진행 현황

```dataview
table 부모RQ, 기능유형, 상태, 담당자
from "SoT/09_Features"
sort 부모RQ asc
```

## RQ 달성 현황

```dataview
table 업무구분, 상태, 담당자
from "SoT/07_Requirements"
where 유형 = "RQ"
sort file.name asc
```

---

## 미결 결정사항

```dataview
table 상태, 생성일, 관련RQ
from "SoT/06_Decisions"
where 상태 = "open"
sort 생성일 desc
```

## 최근 회의

```dataview
table 날짜, 참석자
from "SoT/05_Meetings"
sort 날짜 desc
limit 5
```
