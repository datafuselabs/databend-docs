---
title: H3_EXACT_EDGE_LENGTH_RADS
---

计算这条有向边的长度，单位为弧度。

## 语法

```sql
H3_EXACT_EDGE_LENGTH_RADS(h3)
```

## 示例

```sql
SELECT H3_EXACT_EDGE_LENGTH_KM(1319695429381652479);

┌──────────────────────────────────────────────┐
│ h3_exact_edge_length_km(1319695429381652479) │
├──────────────────────────────────────────────┤
│                            8.267326832647143 │
└──────────────────────────────────────────────┘
```