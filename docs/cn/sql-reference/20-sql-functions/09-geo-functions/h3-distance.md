---
title: H3_DISTANCE
---

返回两个给定的 [H3](https://eng.uber.com/h3/) 索引之间的网格距离。

## 语法

```sql
H3_DISTANCE(h3, a_h3)
```

## 示例

```sql
SELECT H3_DISTANCE(599119489002373119, 599119491149856767);

┌─────────────────────────────────────────────────────┐
│ h3_distance(599119489002373119, 599119491149856767) │
├─────────────────────────────────────────────────────┤
│                                                   1 │
└─────────────────────────────────────────────────────┘
```