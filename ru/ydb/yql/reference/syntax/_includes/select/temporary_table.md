---
sourcePath: ru/ydb/ydb-docs-core/ru/core/yql/reference/yql-core/syntax/_includes/select/temporary_table.md
sourcePath: ru/ydb/yql/reference/yql-core/syntax/_includes/select/temporary_table.md
---

## Явно создаваемые временные (анонимные) таблицы {#temporary-tables}

В сложных многофазных запросах бывает полезно явно создать физическую временную таблицу, чтобы вручную повлиять на ход его выполнения. Для этого можно использовать имя таблицы, начинающееся на `@`. Такие таблицы называются анонимными, чтобы отличать от временных таблиц, создаваемых YT-операцией.

Каждое такое имя в рамках запроса заменяется при выполнении на глобально уникальный путь к таблице во временной директории. Такие временные таблицы автоматически удаляются по завершении выполнения запроса по тем же правилам, как и создаваемые неявно.

Эта функциональность позволяет не заботиться о конфликтах в путях временных таблиц между параллельно работающими операциями, а также не удалять их явно в конце запроса.

**Примеры:**

``` yql
INSERT INTO @my_temp_table
SELECT * FROM my_input_table ORDER BY value;

COMMIT;

SELECT * FROM @my_temp_table WHERE value = "123"
UNION ALL
SELECT * FROM @my_temp_table WHERE value = "456";
```

В имени временной таблицы может использоваться [именованное выражение](../../expressions.md#named-nodes):

``` yql
$tmp_name = "my_temp_table";

INSERT INTO @$tmp_name
SELECT 1 AS one, 2 AS two, 3 AS three;

COMMIT;

SELECT * FROM @$tmp_name;
```