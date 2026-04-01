
## 전체 요구사항

```dataview
table 상태, 담당자, 생성일, 카테고리
from "SoT/01_Requirements"
sort 생성일 desc
```

## 상태별 요구사항 수

```dataview
table length(rows) as "개수"
from "SoT/01_Requirements"
group by 상태
```

## 미결 결정사항

```dataview
table 상태, 생성일, 관련RQ
from "SoT/02_Decisions"
where 상태 = "open"
sort 생성일 desc
```

## 전체 결정사항

```dataview
table 상태, 생성일, 관련RQ
from "SoT/02_Decisions"
sort 생성일 desc
```

## 최근 회의

```dataview
table 날짜, 참석자
from "SoT/03_Meetings"
sort 날짜 desc
limit 10
```
