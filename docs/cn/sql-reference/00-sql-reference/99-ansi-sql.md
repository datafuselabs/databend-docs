---
title: SQL 标准符合程度
---

Databend 的目标是符合 SQL 标准，特别是支持 ISO/IEC 9075:2011，也称为 SQL:2011。虽然这不是完整的符合性声明，但 Databend 包含了 SQL 标准所要求的许多特性，常常在语法或功能上有轻微的差异。本页概述了 Databend 对 SQL:2011 标准的符合程度。

| 特性 ID  |                                   特性名称                                    |                 是否支持                  |                                 注释                                  |
| :------: | :---------------------------------------------------------------------------: | :---------------------------------------: | :-------------------------------------------------------------------: |
| **E011** |                               **数值数据类型**                                |     <span class="text-blue">是</span>     |                                                                       |
| E011-01  |                         INTEGER 和 SMALLINT 数据类型                          |     <span class="text-blue">是</span>     |                                                                       |
| E011-02  |                   REAL, DOUBLE PRECISION 和 FLOAT 数据类型                    |     <span class="text-blue">是</span>     |                                                                       |
| E011-03  |                          DECIMAL 和 NUMERIC 数据类型                          |     <span class="text-blue">是</span>     |                                                                       |
| E011-04  |                                  算术运算符                                   |     <span class="text-blue">是</span>     |                                                                       |
| E011-05  |                                   数值比较                                    |     <span class="text-blue">是</span>     |                                                                       |
| E011-06  |                        在数字数据类型之间进行隐式转换                         |     <span class="text-blue">是</span>     |                                                                       |
| **E021** |                              **字符字符串类型**                               | <span class="text-orange">部分支持</span> |                                                                       |
| E021-01  |                              CHARACTER 数据类型                               |     <span class="text-red">否</span>      |                       不支持固定长度字符串类型                        |
| E021-02  |                          CHARACTER VARYING 数据类型                           |     <span class="text-blue">是</span>     |                                                                       |
| E021-03  |                                 字符串字面量                                  |     <span class="text-blue">是</span>     |                                                                       |
| E021-04  |                             CHARACTER_LENGTH 函数                             |     <span class="text-blue">是</span>     |                                                                       |
| E021-05  |                               OCTET_LENGTH 函数                               |     <span class="text-red">否</span>      |                                                                       |
| E021-06  |                                SUBSTRING 函数                                 |     <span class="text-blue">是</span>     |                                                                       |
| E021-07  |                                  字符串串接                                   |     <span class="text-blue">是</span>     |                                                                       |
| E021-08  |                              UPPER 和 LOWER 函数                              |     <span class="text-blue">是</span>     |                                                                       |
| E021-09  |                                   TRIM 函数                                   |     <span class="text-blue">是</span>     |                                                                       |
| E021-10  |              在固定长度和可变长度字符字符串类型之间进行隐式转换               |     <span class="text-red">否</span>      |                       不支持固定长度字符串类型                        |
| E021-11  |                                 POSITION 函数                                 |     <span class="text-blue">是</span>     |                                                                       |
| E021-12  |                                   字符比较                                    |     <span class="text-blue">是</span>     |                                                                       |
| **E031** |                                  **标识符**                                   |     <span class="text-blue">是</span>     |                                                                       |
| E031-01  |                                  分隔标识符                                   |     <span class="text-blue">是</span>     |                                                                       |
| E031-02  |                                  小写标识符                                   |     <span class="text-blue">是</span>     |                                                                       |
| E031-03  |                                  尾随下划线                                   |     <span class="text-blue">是</span>     |                                                                       |
| **E051** |                               **基本查询规范**                                | <span class="text-orange">部分支持</span> |                                                                       |
| E051-01  |                                SELECT DISTINCT                                |     <span class="text-blue">是</span>     |                                                                       |
| E051-02  |                                 GROUP BY 子句                                 |     <span class="text-blue">是</span>     |                                                                       |
| E051-04  |                     GROUP BY 可包含不在 SELECT 列表中的列                     |     <span class="text-blue">是</span>     |                                                                       |
| E051-05  |                               可以重命名选定项                                |     <span class="text-blue">是</span>     |                                                                       |
| E051-06  |                                  HAVING 子句                                  |     <span class="text-blue">是</span>     |                                                                       |
| E051-07  |      在 SELECT 列表中使用限定符 "\*"，以选择所有列，并指定其所属的表 \*       |     <span class="text-red">否</span>      |                                                                       |
| E051-08  |                             FROM 子句中的关联名称                             |     <span class="text-blue">是</span>     |                                                                       |
| E051-09  |                            在 FROM 子句中重命名列                             |     <span class="text-red">否</span>      |                                                                       |
| **E061** |                            **基本谓词和搜索条件**                             | <span class="text-orange">部分支持</span> |                                                                       |
| E061-01  |                                   比较谓词                                    |     <span class="text-blue">是</span>     |                                                                       |
| E061-02  |                                 BETWEEN 谓词                                  |     <span class="text-blue">是</span>     |                                                                       |
| E061-03  |                               IN 谓词具有值列表                               |     <span class="text-blue">是</span>     |                                                                       |
| E061-04  |                                   LIKE 谓词                                   |     <span class="text-blue">是</span>     |                                                                       |
| E061-05  |                            LIKE 谓词：ESCAPE 子句                             |     <span class="text-red">否</span>      |                                                                       |
| E061-06  |                                   NULL 谓词                                   |     <span class="text-blue">是</span>     |                                                                       |
| E061-07  |                                 量化比较谓词                                  |     <span class="text-blue">是</span>     |                                                                       |
| E061-08  |                                  EXISTS 谓词                                  |     <span class="text-blue">是</span>     |                                                                       |
| E061-09  |                              比较谓词中的子查询                               |     <span class="text-blue">是</span>     |                                                                       |
| E061-11  |                               IN 谓词中的子查询                               |     <span class="text-blue">是</span>     |                                                                       |
| E061-12  |                            量化比较谓词中的子查询                             |     <span class="text-blue">是</span>     |                                                                       |
| E061-13  |                                  相关子查询                                   |     <span class="text-blue">是</span>     |                                                                       |
| E061-14  |                                   搜索条件                                    |     <span class="text-blue">是</span>     |                                                                       |
| **E071** |                              **基本查询表达式**                               | <span class="text-orange">部分支持</span> |                                                                       |
| E071-01  |                            UNION DISTINCT 表操作符                            |     <span class="text-blue">是</span>     |                                                                       |
| E071-02  |                              UNION ALL 表操作符                               |     <span class="text-blue">是</span>     |                                                                       |
| E071-03  |                           EXCEPT DISTINCT 表操作符                            |     <span class="text-blue">是</span>     |                                                                       |
| E071-05  |               通过表操作符组合的列不需要具有完全相同的数据类型                | <span class="text-orange">部分支持</span> |       只有具有可以隐式转换的数据类型的列才允许与表操作符组合。        |
| E071-06  |                              子查询中的表操作符                               |     <span class="text-blue">是</span>     |                                                                       |
| **E081** |                                 **基本权限**                                  | <span class="text-orange">部分支持</span> |                                                                       |
| E081-01  |                             表级别的 SELECT 权限                              |     <span class="text-blue">是</span>     |                                                                       |
| E081-02  |                                  DELETE 权限                                  |     <span class="text-blue">是</span>     |                                                                       |
| E081-03  |                             表级别的 INSERT 权限                              |     <span class="text-blue">是</span>     |                                                                       |
| E081-04  |                             表级别的 UPDATE 权限                              |     <span class="text-blue">是</span>     |                                                                       |
| E081-05  |                             列级别的 UPDATE 权限                              |     <span class="text-red">否</span>      |                                                                       |
| E081-06  |                           表级别的 REFERENCES 权限                            |     <span class="text-red">否</span>      |                                                                       |
| E081-07  |                           列级别的 REFERENCES 权限                            |     <span class="text-red">否</span>      |                                                                       |
| E081-08  |                               WITH GRANT OPTION                               |     <span class="text-red">否</span>      |                                                                       |
| E081-09  |                                  USAGE 权限                                   |     <span class="text-red">否</span>      |                                                                       |
| E081-10  |                                 EXECUTE 权限                                  |     <span class="text-red">否</span>      |                                                                       |
| **E091** |                                 **集合函数**                                  |     <span class="text-blue">是</span>     |                                                                       |
| E091-01  |                                 平均值 (AVG)                                  |     <span class="text-blue">是</span>     |                                                                       |
| E091-02  |                                 计数 (COUNT)                                  |     <span class="text-blue">是</span>     |                                                                       |
| E091-03  |                                 最大值 (MAX)                                  |     <span class="text-blue">是</span>     |                                                                       |
| E091-04  |                                 最小值 (MIN)                                  |     <span class="text-blue">是</span>     |                                                                       |
| E091-05  |                                  总和 (SUM)                                   |     <span class="text-blue">是</span>     |                                                                       |
| E091-06  |                                   ALL 量词                                    |     <span class="text-blue">是</span>     |                                                                       |
| E091-07  |                                 DISTINCT 量词                                 | <span class="text-orange">部分支持</span> | 目前，Databend 支持 COUNT(DISTINCT ...) 和 SELECT DISTINCT ... 查询。 |
| **E101** |                               **基本数据操作**                                | <span class="text-orange">部分支持</span> |                                                                       |
| E101-01  |                                  INSERT 语句                                  |     <span class="text-blue">是</span>     |                                                                       |
| E101-03  |                           带搜索条件的 UPDATE 语句                            |     <span class="text-blue">是</span>     |                                                                       |
| E101-04  |                           带搜索条件的 DELETE 语句                            |     <span class="text-blue">是</span>     |                                                                       |
| **E111** |                             **单行 SELECT 语句**                              |     <span class="text-blue">是</span>     |                                                                       |
| **E121** |                               **基本游标支持**                                | <span class="text-orange">部分支持</span> |                                                                       |
| E121-01  |                                DECLARE CURSOR                                 |     <span class="text-red">否</span>      |                                                                       |
| E121-02  |                        ORDER BY 的列不需要在 SELECT 中                        |     <span class="text-blue">是</span>     |                                                                       |
| E121-03  |                           ORDER BY 子句中的值表达式                           |     <span class="text-blue">是</span>     |                                                                       |
| E121-04  |                                   OPEN 语句                                   |     <span class="text-red">否</span>      |                                                                       |
| E121-06  |                           带位置信息的 UPDATE 语句                            |     <span class="text-red">否</span>      |                                                                       |
| E121-07  |                           带位置信息的 DELETE 语句                            |     <span class="text-red">否</span>      |                                                                       |
| E121-08  |                                  CLOSE 语句                                   |     <span class="text-red">否</span>      |                                                                       |
| E121-10  |                             FETCH 语句：隐式 NEXT                             |     <span class="text-red">否</span>      |                                                                       |
| E121-17  |                                WITH HOLD 游标                                 |     <span class="text-red">否</span>      |                                                                       |
| **E131** |                         **空值支持（代替值的空值）**                          |     <span class="text-blue">是</span>     |                                                                       |
| **E141** |                              **基本完整性约束**                               |     <span class="text-red">否</span>      |                                                                       |
| E141-01  |                                 NOT NULL 约束                                 |     <span class="text-blue">是</span>     |             Databend 默认：所有列都不可为空（NOT NULL）。             |
| E141-02  |                           NOT NULL 列的 UNIQUE 约束                           |     <span class="text-red">否</span>      |                                                                       |
| E141-03  |                               PRIMARY KEY 约束                                |     <span class="text-red">否</span>      |                                                                       |
| E141-04  |    基本 FOREIGN KEY 约束，对于引用删除操作和引用更新操作，默认为 NO ACTION    |     <span class="text-red">否</span>      |                                                                       |
| E141-06  |                                  CHECK 约束                                   |     <span class="text-red">否</span>      |                                                                       |
| E141-07  |                                   列默认值                                    |     <span class="text-blue">是</span>     |                                                                       |
| E141-08  |                            主键上推断出的 NOT NULL                            |     <span class="text-red">否</span>      |                                                                       |
| E141-10  |                        外键中的名称可以以任何顺序指定                         |     <span class="text-red">否</span>      |                                                                       |
| **E151** |                                 **事务支持**                                  | <span class="text-orange">部分支持</span> |                                                                       |
| E151-01  |                                  COMMIT 语句                                  | <span class="text-orange">部分支持</span> |            Databend 只支持每个单独的 DML 语句的隐式事务。             |
| E151-02  |                                 ROLLBACK 语句                                 |     <span class="text-red">否</span>      |                                                                       |
| **E152** |                         **基本 SET TRANSACTION 语句**                         |     <span class="text-red">否</span>      |                                                                       |
| E152-01  |            SET TRANSACTION 语句：ISOLATION LEVEL SERIALIZABLE 子句            |     <span class="text-red">否</span>      |                                                                       |
| E152-02  |              SET TRANSACTION 语句：READ ONLY 和 READ WRITE 子句               |     <span class="text-red">否</span>      |                                                                       |
| **E153** |                          **可更新的含子查询的查询**                           |     <span class="text-blue">是</span>     |                                                                       |
| **E161** |                         **使用前导双减号的 SQL 注释**                         |     <span class="text-blue">是</span>     |                                                                       |
| **E171** |                               **SQLSTATE 支持**                               |     <span class="text-red">否</span>      |                                                                       |
| **E182** |                               **宿主语言绑定**                                |     <span class="text-red">否</span>      |                                                                       |
| **F031** |                               **基本架构操作**                                |     <span class="text-blue">是</span>     |                                                                       |
| F031-01  |                     创建持久化基本表的 CREATE TABLE 语句                      |     <span class="text-blue">是</span>     |                                                                       |
| F031-02  |                               CREATE VIEW 语句                                |     <span class="text-blue">是</span>     |                                                                       |
| F031-03  |                                  GRANT 语句                                   | <span class="text-orange">部分支持</span> |                                                                       |
| F031-04  |                       ALTER TABLE 语句：ADD COLUMN 子句                       |     <span class="text-blue">是</span>     |                                                                       |
| F031-13  |                        DROP TABLE 语句：RESTRICT 子句                         | <span class="text-orange">部分支持</span> |                                                                       |
| F031-16  |                         DROP VIEW 语句：RESTRICT 子句                         | <span class="text-orange">部分支持</span> |                                                                       |
| F031-19  |                          REVOKE 语句：RESTRICT 子句                           | <span class="text-orange">部分支持</span> |                                                                       |
| **F041** |                                **基本联接表**                                 |     <span class="text-blue">是</span>     |                                                                       |
| F041-01  |                       内联接（不一定需要 INNER 关键字）                       |     <span class="text-blue">是</span>     |                                                                       |
| F041-02  |                                 INNER 关键字                                  |     <span class="text-blue">是</span>     |                                                                       |
| F041-03  |                                LEFT OUTER JOIN                                |     <span class="text-blue">是</span>     |                                                                       |
| F041-04  |                               RIGHT OUTER JOIN                                |     <span class="text-blue">是</span>     |                                                                       |
| F041-05  |                               可以嵌套外部联接                                |     <span class="text-blue">是</span>     |                                                                       |
| F041-07  |                     左或右外联接中的内表也可以用于内联接                      |     <span class="text-blue">是</span>     |                                                                       |
| F041-08  |                      支持所有比较操作符（而不仅仅是 = ）                      |     <span class="text-blue">是</span>     |                                                                       |
| **F051** |                              **基本日期和时间**                               | <span class="text-orange">部分支持</span> |                                                                       |
| F051-01  |                     DATE 数据类型（包括支持 DATE 字面量）                     |     <span class="text-blue">是</span>     |                                                                       |
| F051-02  |        TIME 数据类型（包括支持 TIME 字面量）具有至少 0 位的小数秒精度         |     <span class="text-red">否</span>      |                                                                       |
| F051-03  | TIMESTAMP 数据类型（包括支持 TIMESTAMP 字面量）具有至少 0 到 6 位的小数秒精度 |     <span class="text-blue">是</span>     |                                                                       |
| F051-04  |                 对 DATE、TIME 和 TIMESTAMP 数据类型的比较谓词                 |     <span class="text-blue">是</span>     |                                                                       |
| F051-05  |                  日期时间类型与字符字符串类型之间的显式转换                   |     <span class="text-blue">是</span>     |                                                                       |
| F051-06  |                                 CURRENT_DATE                                  |     <span class="text-blue">是</span>     |                                                                       |
| F051-07  |                                   LOCALTIME                                   |     <span class="text-blue">是</span>     |                                                                       |
| F051-08  |                                LOCALTIMESTAMP                                 |     <span class="text-blue">是</span>     |                                                                       |
| **F081** |                         **视图中的 UNION 和 EXCEPT**                          |     <span class="text-blue">是</span>     |                                                                       |
| **E182** |                               **主机语言绑定**                                |     <span class="text-red">否</span>      |                                                                       |
| **F031** |                               **基本架构操作**                                |     <span class="text-blue">是</span>     |                                                                       |
| F031-01  |                     创建持久化基本表的 CREATE TABLE 语句                      |     <span class="text-blue">是</span>     |                                                                       |
| F031-02  |                               CREATE VIEW 语句                                |     <span class="text-blue">是</span>     |                                                                       |
| F031-03  |                                  GRANT 语句                                   | <span class="text-orange">部分支持</span> |                                                                       |
| F031-04  |                       ALTER TABLE 语句：ADD COLUMN 子句                       |     <span class="text-blue">是</span>     |                                                                       |
| F031-13  |                        DROP TABLE 语句：RESTRICT 子句                         | <span class="text-orange">部分支持</span> |                                                                       |
| F031-16  |                         DROP VIEW 语句：RESTRICT 子句                         | <span class="text-orange">部分支持</span> |                                                                       |
| F031-19  |                          REVOKE 语句：RESTRICT 子句                           | <span class="text-orange">部分支持</span> |                                                                       |
| **F041** |                                **基本联接表**                                 |     <span class="text-blue">是</span>     |                                                                       |
| F041-01  |                       内联接（不一定需要 INNER 关键字）                       |     <span class="text-blue">是</span>     |                                                                       |
| F041-02  |                                 INNER 关键字                                  |     <span class="text-blue">是</span>     |                                                                       |
| F041-03  |                                LEFT OUTER JOIN                                |     <span class="text-blue">是</span>     |                                                                       |
| F041-04  |                               RIGHT OUTER JOIN                                |     <span class="text-blue">是</span>     |                                                                       |
| F041-05  |                               可以嵌套外部联接                                |     <span class="text-blue">是</span>     |                                                                       |
| F041-07  |                     左或右外联接中的内表也可以用于内联接                      |     <span class="text-blue">是</span>     |                                                                       |
| F041-08  |                      支持所有比较操作符（而不仅仅是 = ）                      |     <span class="text-blue">是</span>     |                                                                       |
| **F051** |                              **基本日期和时间**                               | <span class="text-orange">部分支持</span> |                                                                       |
| F051-01  |                     DATE 数据类型（包括支持 DATE 字面值）                     |     <span class="text-blue">是</span>     |                                                                       |
| F051-02  |         TIME 数据类型（包括支持 TIME 字面值）具有至少 0 的小数秒精度          |     <span class="text-red">否</span>      |                                                                       |
| F051-03  |  TIMESTAMP 数据类型（包括支持 TIMESTAMP 字面值）具有至少 0 和 6 的小数秒精度  |     <span class="text-blue">是</span>     |                                                                       |
| F051-04  |                 对 DATE、TIME 和 TIMESTAMP 数据类型的比较谓词                 |     <span class="text-blue">是</span>     |                                                                       |
| F051-05  |                  日期时间类型与字符字符串类型之间的显式转换                   |     <span class="text-blue">是</span>     |                                                                       |
| **F081** |                         **视图中的 UNION 和 EXCEPT**                          |     <span class="text-blue">是</span>     |                                                                       |
| **F131** |                                 **分组操作**                                  |     <span class="text-blue">是</span>     |                                                                       |
| F131-01  |           在具有分组视图的查询中支持 WHERE、GROUP BY 和 HAVING 子句           |     <span class="text-blue">是</span>     |                                                                       |
| F131-02  |                       在具有分组视图的查询中支持多个表                        |     <span class="text-blue">是</span>     |                                                                       |
| F131-03  |                      在具有分组视图的查询中支持集合函数                       |     <span class="text-blue">是</span>     |                                                                       |
| F131-04  |               在具有分组视图和 GROUP BY 和 HAVING 子句的子查询                |     <span class="text-blue">是</span>     |                                                                       |
| F131-05  |              具有 GROUP BY 和 HAVING 子句和分组视图的单行 SELECT              |     <span class="text-blue">是</span>     |                                                                       |
| **F181** |                                **多模块支持**                                 |     <span class="text-red">否</span>      |                                                                       |
| **F201** |                                 **CAST 函数**                                 |     <span class="text-blue">是</span>     |                                                                       |
| **F221** |                                **显式默认值**                                 |     <span class="text-red">否</span>      |                                                                       |
| **F261** |                                **CASE 表达式**                                |     <span class="text-blue">是</span>     |                                                                       |
| F261-01  |                                   简单 CASE                                   |     <span class="text-blue">是</span>     |                                                                       |
| F261-02  |                               带搜索条件的 CASE                               |     <span class="text-blue">是</span>     |                                                                       |
| F261-03  |                                    NULLIF                                     |     <span class="text-blue">是</span>     |                                                                       |
| F261-04  |                                   COALESCE                                    |     <span class="text-blue">是</span>     |                                                                       |
| **F311** |                               **架构定义语句**                                | <span class="text-orange">部分支持</span> |                                                                       |
| F311-01  |                                 CREATE SCHEMA                                 |     <span class="text-blue">是</span>     |                                                                       |
| F311-02  |                        创建持久化基本表的 CREATE TABLE                        |     <span class="text-blue">是</span>     |                                                                       |
| F311-03  |                                  CREATE VIEW                                  |     <span class="text-blue">是</span>     |                                                                       |
| F311-04  |                        CREATE VIEW: WITH CHECK OPTION                         |     <span class="text-red">否</span>      |                                                                       |
| F311-05  |                                  GRANT 语句                                   | <span class="text-orange">部分支持</span> |                                                                       |
| **F471** |                               **标量子查询值**                                |     <span class="text-blue">是</span>     |                                                                       |
| **F481** |                              **扩展 NULL 谓词**                               |     <span class="text-blue">是</span>     |                                                                       |
| **F812** |                                 **基本标记**                                  |     <span class="text-red">否</span>      |                                                                       |
| **S011** |                              **不同的数据类型**                               |     <span class="text-red">否</span>      |                                                                       |
| **T321** |                            **基本 SQL 调用的例程**                            |     <span class="text-red">否</span>      |                                                                       |
| T321-01  |                             不重载的用户定义函数                              |     <span class="text-blue">是</span>     |                                                                       |
| T321-02  |                           不重载的用户定义存储过程                            |     <span class="text-red">否</span>      |                                                                       |
| T321-03  |                                   函数调用                                    |     <span class="text-blue">是</span>     |                                                                       |
| T321-04  |                                   CALL 语句                                   |     <span class="text-red">否</span>      |                                                                       |
| T321-05  |                                  RETURN 语句                                  |     <span class="text-red">否</span>      |                                                                       |
| **T631** |                        **带有单个列表元素的 IN 谓词**                         |     <span class="text-blue">是</span>     |                                                                       |
