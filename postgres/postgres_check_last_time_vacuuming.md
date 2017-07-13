#  How to check for the last time VACUUM was executed

Running vacuuming on a regular basis is essential for the postgres database and also recommended by the postgres manual, see
[https://www.postgresql.org/docs/current/static/routine-vacuuming.html](https://www.postgresql.org/docs/current/static/routine-vacuuming.html)

To check the last times tables got vacuumed, use the query below

```
SELECT relname, last_vacuum, last_autovacuum, last_analyze, last_autoanalyze
FROM pg_stat_all_tables
WHERE schemaname = 'public';
```
