---
layout: post
title: "通过SQL文件创建Sqlite3数据库"
description: "create sqlite3 db from sql file"
keywords: "sqlite3, linux, sql, database"
category: "Linux"
tags: [Linux, Database]
---
{% include JB/setup %}

在某些嵌入式应用中，需要使用数据库来保存数据，为了避免在程序中去初始化数据库，可以通过sql文件在启动脚本中生成相应数据库文件:

``
sqlite3 /tmp/test.db < test_create.sql
``

<!-- more -->
``test_create.sql``是标准的SQL文件，如:

``` sql
CREATE TABLE test (
    num     INTEGER PRIMARY KEY,
    city    TEXT
);
```

还可以将默认数据放在另外一个sql文件中，如``test_data.sql``:

``` sql
BEGIN TRANSACTION;

INSERT INTO test(num, city) VALUES(028, 'Chengdu');

COMMIT;
```

通过命令将数据添加到数据库中``sqlite3 /tmp/test.db < test_data.sql``.



####Note:
数据库文件夹的路径必须存在，如果不存在会导致文件创建失败。
