---
title: TO_WEEK_OF_YEAR
---
import FunctionDescription from '@site/src/components/FunctionDescription';

<FunctionDescription description="引入或更新: v1.2.151"/>

计算给定日期在一年中的周数。

ISO 周数计算方式如下：1月4日始终被视为第一周的一部分。如果1月1日是星期四，则从12月29日星期一到1月4日星期日的周被指定为ISO周1。如果1月1日是星期五，则从1月4日星期一到1月10日星期日的周被标记为ISO周1。

## 语法

```sql
TO_WEEK_OF_YEAR(<expr>)
```

## 参数

| 参数       | 描述         |
|-----------|--------------|
| `<expr>`  | 日期/时间戳  |

## 别名

- [WEEK](week.md)
- [WEEKOFYEAR](weekofyear.md)

## 返回类型

返回一个整数，表示一年中的周数，范围从1到53。

## 示例

```sql
SELECT NOW(), TO_WEEK_OF_YEAR(NOW()), WEEK(NOW()), WEEKOFYEAR(NOW());

┌───────────────────────────────────────────────────────────────────────────────────────┐
│            now()           │ to_week_of_year(now()) │ week(now()) │ weekofyear(now()) │
├────────────────────────────┼────────────────────────┼─────────────┼───────────────────┤
│ 2024-03-14 23:30:04.011624 │                     11 │          11 │                11 │
└───────────────────────────────────────────────────────────────────────────────────────┘
```