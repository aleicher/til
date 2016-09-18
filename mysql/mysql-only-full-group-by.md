#MySQL mode ONLY_FULL_GROUP_BY

When set, mysql will reject queries for which the select list, HAVING condition, or ORDER BY list refer to nonaggregated columns that are neither named in the GROUP BY clause nor are functionally dependent on (uniquely determined by) GROUP BY columns.

As of MySQL 5.7.5, the default SQL mode includes ONLY_FULL_GROUP_BY. 

To disable it, manually, first connect to the mysql database and get the current global `sql_mode` settings:

`SELECT @@GLOBAL.sql_mode;`

and set them then using:

`SET GLOBAL sql_mode = 'modes'`

Example:
```
mysql> SELECT @@GLOBAL.sql_mode;
+-------------------------------------------------------------------------------------------------------------------------------------------+
| @@GLOBAL.sql_mode                                                                                                                         |
+-------------------------------------------------------------------------------------------------------------------------------------------+
| ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION |
+-------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```

now, remove the first entry: `ONLY_FULL_GROUP_BY`
and set the `sql_mode`:

```
mysql> SET GLOBAL sql_mode = 'STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
```

```
mysql> SELECT @@GLOBAL.sql_mode;
+------------------------------------------------------------------------------------------------------------------------+
| @@GLOBAL.sql_mode                                                                                                      |
+------------------------------------------------------------------------------------------------------------------------+
| STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION |
+------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```


## Alternative: config file

As an alternative create a config file in `/etc/mysql/conf.d/my.cnf`

```
# filename: my.cnf
[mysqld]
sql-mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"

```
note that in this file, `"` are used instead of the `'` inside the mysql shell, and no `;` is provided at the end of the line
