---
title: TO_TIMESTAMP
---
import FunctionDescription from '@site/src/components/FunctionDescription';

<FunctionDescription description="引入或更新: v1.2.575"/>

将表达式转换为带时间的日期。

另请参阅: [TO_DATE](to-date)

## 语法

```sql
-- 将字符串或整数转换为时间戳
TO_TIMESTAMP(<expr>)
```

如果给定一个 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 日期格式字符串，该函数从字符串中提取日期；如果给定的是一个整数，该函数将整数解释为自 Unix 纪元（1970 年 1 月 1 日午夜）以来的秒数、毫秒数或微秒数（负数表示之前，正数表示之后）：

| 范围                                       | 单位                 |
|---------------------------------------------|----------------------|
| x < 31,536,000,000                          | 秒                   |
| 31,536,000,000 ≤ x < 31,536,000,000,000     | 毫秒                 |
| x ≥ 31,536,000,000,000                      | 微秒                 |

```sql
-- 使用给定模式将字符串转换为时间戳
TO_TIMESTAMP(<expr>, <pattern>)
```

如果给定两个参数，该函数根据第二个字符串中指定的模式将第一个字符串转换为时间戳。要指定模式，请使用说明符。说明符允许您定义所需的日期和时间格式。有关支持的说明符的完整列表，请参阅 [日期和时间格式化](../../00-sql-reference/10-data-types/20-data-type-time-date-types.md#formatting-date-and-time)。

## 返回类型

返回一个格式为 `YYYY-MM-DD hh:mm:ss.ffffff` 的时间戳：

- 返回的时间戳始终反映您的 Databend 时区。
    - 当给定字符串中包含时区信息时，它将时间戳转换为 Databend 配置的时区对应的时间。换句话说，它会调整时间戳以反映 Databend 中设置的时区。

    ```sql
    -- 设置时区为 'America/Toronto' (UTC-5:00, 东部标准时间)
    SET timezone = 'America/Toronto';

    SELECT TO_TIMESTAMP('2022-01-02T01:12:00-07:00'), TO_TIMESTAMP('2022/01/02T01:12:00-07:00', '%Y/%m/%dT%H:%M:%S%::z');

    ┌────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
    │ to_timestamp('2022-01-02t01:12:00-07:00') │ to_timestamp('2022/01/02t01:12:00-07:00', '%y/%m/%dt%h:%m:%s%::z') │
    ├───────────────────────────────────────────┼────────────────────────────────────────────────────────────────────┤
    │ 2022-01-02 03:12:00                       │ 2022-01-02 03:12:00                                                │
    └────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
    ```

    - 如果给定字符串中不包含时区信息，它将假定时间戳属于当前会话配置的时区。

    ```sql
    -- 设置时区为 'America/Toronto' (UTC-5:00, 东部标准时间)
    SET timezone = 'America/Toronto';
    
    SELECT TO_TIMESTAMP('2022-01-02T01:12:00'), TO_TIMESTAMP('2022/01/02T01:12:00', '%Y/%m/%dT%H:%M:%S');

    ┌────────────────────────────────────────────────────────────────────────────────────────────────┐
    │ to_timestamp('2022-01-02t01:12:00') │ to_timestamp('2022/01/02t01:12:00', '%y/%m/%dt%h:%m:%s') │
    ├─────────────────────────────────────┼──────────────────────────────────────────────────────────┤
    │ 2022-01-02 01:12:00                 │ 2022-01-02 01:12:00                                      │
    └────────────────────────────────────────────────────────────────────────────────────────────────┘
    ```

- 如果给定字符串匹配此格式但没有时间部分，它会自动扩展为此模式。填充值为 0。
- 如果转换失败，将返回错误。为了避免此类错误，您可以使用 [TRY_TO_TIMESTAMP](try-to-timestamp.md) 函数。

    ```sql
    root@localhost:8000/default> SELECT TO_TIMESTAMP('20220102');
    error: APIError: ResponseError with 1006: cannot parse to type `TIMESTAMP` while evaluating function `to_timestamp('20220102')`

    root@localhost:8000/default> SELECT TRY_TO_TIMESTAMP('20220102');

    SELECT
    try_to_timestamp('20220102')

    ┌──────────────────────────────┐
    │ try_to_timestamp('20220102') │
    ├──────────────────────────────┤
    │ NULL                         │
    └──────────────────────────────┘
    ```

## 别名

- [TO_DATETIME](to-datetime.md)
- [STR_TO_TIMESTAMP](str-to-timestamp.md)

## 示例

### 示例-1: 将字符串转换为时间戳

```sql
SELECT TO_TIMESTAMP('2022-01-02 02:00:11');

┌─────────────────────────────────────┐
│ to_timestamp('2022-01-02 02:00:11') │
├─────────────────────────────────────┤
│ 2022-01-02 02:00:11                 │
└─────────────────────────────────────┘

SELECT TO_TIMESTAMP('2022-01-02T01');

┌───────────────────────────────┐
│ to_timestamp('2022-01-02t01') │
├───────────────────────────────┤
│ 2022-01-02 01:00:00           │
└───────────────────────────────┘

-- 设置时区为 'America/Toronto' (UTC-5:00, 东部标准时间)
SET timezone = 'America/Toronto';
-- 将提供的字符串转换为当前时区 ('America/Toronto')
SELECT TO_TIMESTAMP('2022-01-02T01:12:00-07:00');

┌───────────────────────────────────────────┐
│ to_timestamp('2022-01-02t01:12:00-07:00') │
├───────────────────────────────────────────┤
│ 2022-01-02 03:12:00                       │
└───────────────────────────────────────────┘
```

### 示例-2: 将整数转换为时间戳

```sql
SELECT TO_TIMESTAMP(1), TO_TIMESTAMP(-1);

┌───────────────────────────────────────────┐
│   to_timestamp(1)   │  to_timestamp(- 1)  │
├─────────────────────┼─────────────────────┤
│ 1969-12-31 19:00:01 │ 1969-12-31 18:59:59 │
└───────────────────────────────────────────┘
```

您还可以将整数字符串转换为时间戳：

```sql
SELECT TO_TIMESTAMP(TO_INT64('994518299'));

┌─────────────────────────────────────┐
│ to_timestamp(to_int64('994518299')) │
├─────────────────────────────────────┤
│ 2001-07-07 15:04:59                 │
└─────────────────────────────────────┘
```

:::note
- 您也可以使用 `SELECT TO_TIMESTAMP('994518299', '%s')` 进行转换，但不推荐。对于此类转换，Databend 建议使用上述示例中的方法以获得更好的性能。

- 时间戳值范围从 1000-01-01 00:00:00.000000 到 9999-12-31 23:59:59.999999。如果您运行以下语句，Databend 将返回错误：

```bash
root@localhost:8000/default> SELECT TO_TIMESTAMP(9999999999999999999);
error: APIError: ResponseError with 1006: number overflowed while evaluating function `to_int64(9999999999999999999)`
```
:::

### 示例-3: 使用模式将字符串转换为时间戳

```sql
-- 设置时区为 'America/Toronto' (UTC-5:00, 东部标准时间)
SET timezone = 'America/Toronto';

-- 将提供的字符串转换为当前时区 ('America/Toronto')
SELECT TO_TIMESTAMP('2022/01/02T01:12:00-07:00', '%Y/%m/%dT%H:%M:%S%::z');

┌────────────────────────────────────────────────────────────────────┐
│ to_timestamp('2022/01/02t01:12:00-07:00', '%y/%m/%dt%h:%m:%s%::z') │
├────────────────────────────────────────────────────────────────────┤
│ 2022-01-02 03:12:00                                                │
└────────────────────────────────────────────────────────────────────┘

-- 如果未指定时区，则应用会话的时区。
SELECT TO_TIMESTAMP('2022/01/02T01:12:00', '%Y/%m/%dT%H:%M:%S');

┌──────────────────────────────────────────────────────────┐
│ to_timestamp('2022/01/02t01:12:00', '%y/%m/%dt%h:%m:%s') │
├──────────────────────────────────────────────────────────┤
│ 2022-01-02 01:12:00                                      │
└──────────────────────────────────────────────────────────┘
```