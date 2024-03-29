---
title: 日期与时间
description: 基本日期和时间数据类型。
---

## 日期和时间数据类型

|  名称      | 别名       | 存储大小 |  分辨率      | 最小值                | 最大值                          | 描述
|----------- | --------- |  ----------- | -------------|-----------------------| -----------------------------  |
|  DATE      |           | 4 字节      |  天          | 1000-01-01            | 9999-12-31                     | YYYY-MM-DD             |
|  TIMESTAMP |  DATETIME | 8 字节      |  微秒        | 1000-01-01 00:00:00   | 9999-12-31 23:59:59.999999 UTC | YYYY-MM-DD hh:mm:ss[.fraction]，精确到微秒（6位数字）

## 示例

```sql
CREATE TABLE test_dt
  (
     date DATE,
     ts   TIMESTAMP
  );
```
```sql
DESC test_dt;
```

结果:
```
┌────────────────────────────────────────────────┐
│  字段 │    类型   │  空值  │ 默认值 │  额外信息 │
├────────┼───────────┼────────┼─────────┼────────┤
│ date   │ DATE      │ YES    │ NULL    │        │
│ ts     │ TIMESTAMP │ YES    │ NULL    │        │
└────────────────────────────────────────────────┘
```

TIMESTAMP 值可以可选地包含一个尾随的小数秒部分，精确到微秒（6位数字）。

```sql
-- 向表中插入值
INSERT INTO test_dt
VALUES
  ('2022-04-07', '2022-04-07 01:01:01.123456'),
  ('2022-04-08', '2022-04-08 01:01:01');

SELECT *
FROM test_dt;
```

结果:
```
┌─────────────────────────────────────────────┐
│      date      │             ts             │
├────────────────┼────────────────────────────┤
│ 2022-04-07     │ 2022-04-07 01:01:01.123456 │
│ 2022-04-08     │ 2022-04-08 01:01:01        │
└─────────────────────────────────────────────┘
```

Databend 识别多种格式的 TIMESTAMP 值。

```sql
-- 创建一个表来测试不同的时间戳格式
CREATE TABLE test_formats (
    id INT,
    a TIMESTAMP
);

-- 使用不同的时间戳格式插入值
INSERT INTO test_formats
VALUES 
    (1, '2022-01-01 02:00:11'),
    (2, '2022-01-02T02:00:22'),
    (3, '2022-02-02T04:00:03+00:00'),
    (4, '2022-02-03');
```

```sql
SELECT *
FROM test_formats;

```
结果:
```
┌───────────────────────────────────────┐
│        id       │          a          │
├─────────────────┼─────────────────────┤
│               1 │ 2022-01-01 02:00:11 │
│               2 │ 2022-01-02 02:00:22 │
│               3 │ 2022-02-02 04:00:03 │
│               4 │ 2022-02-03 00:00:00 │
└───────────────────────────────────────┘
```

Databend 根据您当前的时区自动调整并显示 TIMESTAMP 值。

```sql
-- 创建一个表来测试带时区调整的时间戳值
CREATE TABLE test_tz (
    id INT,
    t TIMESTAMP
);

-- 将时区设置为 UTC
SET timezone = 'UTC';

-- 插入考虑不同时区的时间戳值
INSERT INTO test_tz
VALUES 
    (1, '2022-02-03T03:00:00'),
    (2, '2022-02-03T03:00:00+08:00'),
    (3, '2022-02-03T03:00:00-08:00'),
    (4, '2022-02-03'),
    (5, '2022-02-03T03:00:00+09:00'),
    (6, '2022-02-03T03:00:00+06:00');
```

```
SELECT *
FROM test_tz;
```
结果:
```
┌───────────────────────────────────────┐
│        id       │          t          │
├─────────────────┼─────────────────────┤
│               1 │ 2022-02-03 03:00:00 │
│               2 │ 2022-02-02 19:00:00 │
│               3 │ 2022-02-03 11:00:00 │
│               4 │ 2022-02-03 00:00:00 │
│               5 │ 2022-02-02 18:00:00 │
│               6 │ 2022-02-02 21:00:00 │
└───────────────────────────────────────┘
```

```sql
-- 将时区更改为亚洲/上海
SET timezone = 'Asia/Shanghai';

-- 使用新的时区设置从表中选择数据
SELECT *
FROM test_tz;
```

结果:
```
┌───────────────────────────────────────┐
│        id       │          t          │
├─────────────────┼─────────────────────┤
│               1 │ 2022-02-03 11:00:00 │
│               2 │ 2022-02-03 03:00:00 │
│               3 │ 2022-02-03 19:00:00 │
│               4 │ 2022-02-03 08:00:00 │
│               5 │ 2022-02-03 02:00:00 │
│               6 │ 2022-02-03 05:00:00 │
└───────────────────────────────────────┘
```

## 函数

参见 [日期与时间函数](/sql/sql-functions/datetime-functions).

### 格式化日期和时间

在 Databend 中，某些日期和时间函数，如 [TO_DATE](../../20-sql-functions/05-datetime-functions/to-date.md) 和 [TO_TIMESTAMP](../../20-sql-functions/05-datetime-functions/to-timestamp.md)，要求您指定日期和时间值的所需格式。为了处理日期和时间格式化，Databend 使用了 chrono 库中提供的标准模块 chrono::format::strftime。这个模块使得对日期和时间的格式化控制变得非常精确。以下内容摘自 https://docs.rs/chrono/latest/chrono/format/strftime/index.html ：

| 规范  | 示例                             | 描述                                                                                                                                                                                 |
|-------|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       |                                  | 日期指示符：                                                                                                                                                                         |
| %Y    | 2001                             | 完整的公历年份，补零至4位数字。chrono 支持从 -262144 到 262143 年。注意：公元前1年或公元后9999年之前的年份，需要一个初始符号（+/-）。                                                  |
| %C    | 20                               | 公历年份除以100，补零至2位数字。                                                                                                                                                      |
| %y    | 01                               | 公历年份取模100，补零至2位数字。                                                                                                                                                      |
| %m    | 07                               | 月份号码（01–12），补零至2位数字。                                                                                                                                                    |
| %b    | Jul                              | 缩写月份名称。始终为3个字母。                                                                                                                                                         |
| %B    | July                             | 完整月份名称。解析时也接受相应的缩写。                                                                                                                                                |
| %h    | Jul                              | 与 %b 相同。                                                                                                                                                                         |
| %d    | 08                               | 日号码（01–31），补零至2位数字。                                                                                                                                                      |
| %e    |  8                               | 与 %d 相同，但用空格填充。与 %_d 相同。                                                                                                                                               |
| %a    | Sun                              | 缩写星期名称。始终为3个字母。                                                                                                                                                         |
| %A    | Sunday                           | 完整星期名称。解析时也接受相应的缩写。                                                                                                                                                |
| %w    | 0                                | 星期日 = 0，星期一 = 1，…，星期六 = 6。                                                                                                                                               |
| %u    | 7                                | 星期一 = 1，星期二 = 2，…，星期日 = 7。（ISO 8601）                                                                                                                                   |
| %U    | 28                               | 以星期日开始的周数（00–53），补零至2位数字。                                                                                                                                          |
| %W    | 27                               | 与 %U 相同，但第1周从该年的第一个星期一开始。                                                                                                                                         |
| %G    | 2001                             | 与 %Y 相同，但使用 ISO 8601 周日期中的年份号码。                                                                                                                                      |
| %g    | 01                               | 与 %y 相同，但使用 ISO 8601 周日期中的年份号码。                                                                                                                                      |
| %V    | 27                               | 与 %U 相同，但使用 ISO 8601 周日期中的周数（01–53）。                                                                                                                                 |
| %j    | 189                              | 年中的日号（001–366），补零至3位数字。                                                                                                                                                |
| %D    | 07/08/01                         | 月-日-年格式。与 %m/%d/%y 相同。                                                                                                                                                      |
| %x    | 07/08/01                         | 本地日期表示（例如，12/31/99）。                                                                                                                                                      |
| %F    | 2001-07-08                       | 年-月-日格式（ISO 8601）。与 %Y-%m-%d 相同。                                                                                                                                          |
| %v    |  8-Jul-2001                      | 日-月-年格式。与 %e-%b-%Y 相同。                                                                                                                                                      |
|       |                                  | 时间指示符：                                                                                                                                                                         |
| %H    | 00                               | 小时数（00–23），补零至2位数字。                                                                                                                                                      |
| %k    |  0                               | 与 %H 相同，但用空格填充。与 %_H 相同。                                                                                                                                               |
| %I    | 12                               | 12小时制的小时数（01–12），补零至2位数字。                                                                                                                                            |
| %l    | 12                               | 与 %I 相同，但用空格填充。与 %_I 相同。                                                                                                                                               |
| %P    | am                               | 12小时制中的 am 或 pm。                                                                                                                                                              |
| %p    | AM                               | 12小时制中的 AM 或 PM。                                                                                                                                                              |
| %M    | 34                               | 分钟数（00–59），补零至2位数字。                                                                                                                                                      |
| %S    | 60                               | 秒数（00–60），补零至2位数字。                                                                                                                                                        |
| %f    | 026490000                        | 自上一整秒以来的分数秒（以纳秒为单位）。                                                                                                                                              |
| %.f   | .026490                          | 与 .%f 类似，但左对齐。这些都消耗了前导点。                                                                                                                                           |
| %.3f  | .026                             | 与 .%f 类似，但左对齐且长度固定为3。                                                                                                                                                 |
| %.6f  | .026490                          | 与 .%f 类似，但左对齐且长度固定为6。                                                                                                                                                 |
| %.9f  | .026490000                       | 与 .%f 类似，但左对齐且长度固定为9。                                                                                                                                                 |
| %3f   | 026                              | 与 %.3f 类似，但没有前导点。                                                                                                                                                         |
| %6f   | 026490                           | 与 %.6f 类似，但没有前导点。                                                                                                                                                         |
| %9f   | 026490000                        | 与 %.9f 类似，但没有前导点。                                                                                                                                                         |
| %R    | 00:34                            | 小时-分钟格式。与 %H:%M 相同。                                                                                                                                                       |
| %T    | 00:34:60                         | 小时-分钟-秒格式。与 %H:%M:%S 相同。                                                                                                                                                 |
| %X    | 00:34:60                         | 本地时间表示（例如，23:13:48）。                                                                                                                                                     |
| %r    | 12:34:60 AM                      | 12小时制的小时-分钟-秒格式。与 %I:%M:%S %p 相同。                                                                                                                                     |
|       |                                  | 时区指示符：                                                                                                                                                                         |
| %Z    | ACST                             | 本地时区名称。解析时跳过所有非空白字符。                                                                                                                                              |
| %z    | +0930                            | 与本地时间相对于 UTC 的偏移量（UTC 为 +0000）。                                                                                                                                       |
| %:z   | +09:30                           | 与 %z 相同，但带有冒号。                                                                                                                                                              |
| %::z  | +09:30:00                        | 与本地时间相对于 UTC 的偏移量，包括秒数。                                                                                                                                             |
| %:::z | +09                              | 与本地时间相对于 UTC 的偏移量，不包括分钟。                                                                                                                                           |
| %#z   | +09                              | 仅解析：与 %z 相同，但允许分钟缺失或存在。                                                                                                                                           |
|       |                                  | 日期和时间指示符：                                                                                                                                                                   |
| %c    | Sun Jul  8 00:34:60 2001         | 本地日期和时间（例如，Thu Mar 3 23:05:25 2005）。                                                                                                                                    |
| %+    | 2001-07-08T00:34:60.026490+09:30 | ISO 8601 / RFC 3339 日期和时间格式。                                                                                                                                                |
| %s    | 994518299                        | UNIX 时间戳，自1970-01-01 00:00 UTC起的秒数。                                                                                                                                        |
|       |                                  | 特殊指示符：                                                                                                                                                                         |
| %t    |                                  | 字面制表符（\t）。                                                                                                                                                                   |
| %n    |                                  | 字面换行符（\n）。                                                                                                                                                                   |
| %%    |                                  | 字面百分号。                                                                                                                                                                         |

可以覆盖数字指示符 %? 的默认填充行为。这不允许用于其他指示符，否则会导致 BAD_FORMAT 错误。

| 修饰符 | 描述                                                                             |
|--------|---------------------------------------------------------------------------------|
| %-?    | 抑制包括空格和零在内的任何填充。（例如 %j = 012, %-j = 12）                      |
| %_?    | 使用空格作为填充。（例如 %j = 012, %_j =  12）                                   |
| %0?    | 使用零作为填充。（例如 %e =  9, %0e = 09）                                       |

- %C, %y：这是向下取整，所以公元前100年（年份编号 -99）将打印为 -1 和 99。

- %U：第1周从那年的第一个星期日开始。在第一个星期日之前的日子可能有第0周。

- %G, %g, %V：第1周是那年至少有4天的第一周。不存在第0周，因此应该与 %G 或 %g 一起使用。

- %S：它考虑了闰秒，所以 60 是可能的。

- %f, %.f, %.3f, %.6f, %.9f, %3f, %6f, %9f：
  默认的 %f 是右对齐的，并且总是用零填充到9位数字，以与 glibc 等兼容，因此它总是计算自上一个整秒以来的纳秒数。例如，在上一个秒之后的7毫秒将打印 007000000，解析 7000000 将产生相同的结果。

  变体 %.f 是左对齐的，并根据精度打印 0、3、6 或 9 位小数位。例如，在上一个秒之后的70毫秒下的 %.f 将打印 .070（注意：不是 .07），解析 .07、.070000 等将产生相同的结果。注意，如果小数部分为零或下一个字符不是 .，它们可以不打印或读取任何内容。

  变体 %.3f、%.6f 和 %.9f 是左对齐的，并根据 f 前面的数字打印 3、6 或 9 位小数位。例如，在上一个秒之后的70毫秒下的 %.3f 将打印 .070（注意：不是 .07），解析 .07、.070000 等将产生相同的结果。注意，如果小数部分为零或下一个字符不是 .，它们可以不读取任何内容，但会按指定长度打印。

  变体 %3f、%6f 和 %9f 是左对齐的，并根据 f 前面的数字打印 3、6 或 9 位小数位，但没有前导点。例如，在上一个秒之后的70毫秒下的 %3f 将打印 070（注意：不是 07），解析 07、070000 等将产生相同的结果。注意，如果小数部分为零，它们可以不读取任何内容。

- %Z：从解析的数据中不会填充偏移量，也不会进行验证。时区完全被忽略。类似于 glibc strptime 对此格式代码的处理。

  无法可靠地从缩写转换为偏移量，例如 CDT 可以表示北美的中央夏令时间或中国夏令时间。

- %+：与 %Y-%m-%dT%H:%M:%S%.f%:z 相同，即秒的小数位为 0、3、6 或 9 位，时区偏移中的冒号。

  此格式还支持在 %:z 的位置使用 Z 或 UTC。它们等同于 +00:00。

  注意，所有的 T、Z 和 UTC 都是不区分大小写解析的。

  典型的 strftime 实现对此指示符有不同的（且依赖于地区的）格式。虽然 Chrono 的 %+ 格式更稳定，但如果您想控制确切的输出，最好避免使用此指示符。

- %s：这不是填充的，可以是负数。就 Chrono 而言，它只考虑非闰秒，因此与 ISO C strftime 行为略有不同。