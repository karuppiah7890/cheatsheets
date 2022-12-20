# Postgres

This is my cheatsheet for anything related to Postgres

1. How do I list all the databases?

```
psql> \l
```

2. How do I list all the tables?

```
psql> \dt
```

To see table size and description use

```
psql> \dt+
```

3. How do I see the rows in a table when the row values are too big or if
number of columns is a lot and the table (view) is distorted?

Try the expanded display toggle option

```
psql> select * from sample;
   id   |         created_at
--------+----------------------------
 754777 | 2020-03-24 06:16:58.750022
 152895 | 2020-03-24 06:17:00.48341
 487637 | 2020-03-24 06:17:01.431379
 240905 | 2020-03-24 06:17:09.620083
 534991 | 2020-03-24 06:17:10.927594
 843870 | 2020-03-24 06:17:12.933908
 878890 | 2020-03-24 06:17:14.940175
  81087 | 2020-03-24 06:17:16.946306
 851699 | 2020-03-24 06:17:18.961483
 679228 | 2020-03-24 06:17:41.285472
  62376 | 2020-03-24 06:17:44.097911
 317611 | 2020-03-24 06:17:46.106755

psql> \x
Expanded display is on.

psql> select * from sample;
-[ RECORD 1 ]--------------------------
id         | 754777
created_at | 2020-03-24 06:16:58.750022
-[ RECORD 2 ]--------------------------
id         | 152895
created_at | 2020-03-24 06:17:00.48341
-[ RECORD 3 ]--------------------------
id         | 487637
created_at | 2020-03-24 06:17:01.431379
-[ RECORD 4 ]--------------------------
id         | 240905
created_at | 2020-03-24 06:17:09.620083
-[ RECORD 5 ]--------------------------
id         | 534991

psql> \x
Expanded display is off.

```

4. How do I connect to another database from my current database in psql?

```
postgres=# \conninfo
You are connected to database "postgres" as user "karuppiah" on host "localhost" at port "5432".

postgres=# \l

                                                    List of databases
        Name        |       Owner        | Encoding |  Collate   |   Ctype    |             Access privileges
--------------------+--------------------+----------+------------+------------+-------------------------------------------
 karuppiah          | karuppiah          | UTF8     | en_US.utf8 | en_US.utf8 |
 postgres           | karuppiah          | UTF8     | en_US.utf8 | en_US.utf8 |
 template0          | karuppiah          | UTF8     | en_US.utf8 | en_US.utf8 | =c/karuppiah                    +
                    |                    |          |            |            | karuppiah=CTc/karuppiah
 template1          | karuppiah          | UTF8     | en_US.utf8 | en_US.utf8 | =c/karuppiah                    +
                    |                    |          |            |            | karuppiah=CTc/karuppiah
(4 rows)

postgres=# \c karuppiah
You are now connected to database "karuppiah" as user "karuppiah".

karuppiah=# \conninfo
You are connected to database "karuppiah" as user "karuppiah" on host "localhost" at port "5432".

```

5. How do I find the server version?

```
select * from pg_settings where name='server_version';
```

Example -

```
postgres=# \x
Expanded display is on.
postgres=# select * from pg_settings where name='server_version';
-[ RECORD 1 ]---+--------------------------
name            | server_version
setting         | 14.4
unit            | 
category        | Preset Options
short_desc      | Shows the server version.
extra_desc      | 
context         | internal
vartype         | string
source          | default
min_val         | 
max_val         | 
enumvals        | 
boot_val        | 14.4
reset_val       | 14.4
sourcefile      | 
sourceline      | 
pending_restart | f
```

6. Streaming Replication related SQL queries

See https://www.postgresql.org/docs/current/functions-admin.html#FUNCTIONS-REPLICATION for current docs or https://www.postgresql.org/docs/14/functions-admin.html under `Replication Management Functions` section

```sql
select * from pg_replication_slots;
```

```sql
select * from pg_stat_replication;
```

```sql
-- the second argument is for "immediately_reserver"
select pg_create_physical_replication_slot('replication_slot_name', true);
```

```sql
-- advancing to current Log Sequence Number (LSN),
-- assuming the slot has a restart_lsn defined or else it will error out saying
-- ERROR:  replication slot "replication_slot_name" cannot be advanced
-- DETAIL:  This slot has never previously reserved WAL, or it has been invalidated.
select pg_replication_slot_advance('replication_slot_name', pg_current_wal_lsn());
```

```sql
select pg_wal_lsn_diff(pg_current_wal_lsn(), (select restart_lsn from pg_replication_slots where slot_name='<replication_slot_name>'));
```

```sql
select pg_current_wal_insert_lsn();
```

```sql
select * from pg_stat_replication_slots;
```

```sql
\sf pg_get_replication_slots
```

```sql
\sf+ pg_get_replication_slots
```

```sql
\sf pg_replication_slot_advance
```

```sql
\sv pg_replication_slots
```

```sql
\dv pg_replication_slots
```

```sql
\dv+ pg_replication_slots
```

```sql
SELECT * from pg_replication_slots WHERE active = False ORDER BY restart_lsn DESC;
```

```sql
select pg_last_xact_replay_timestamp();
```

```sql
select pg_last_wal_replay_lsn();
```

```sql
select pg_last_wal_receive_lsn();
```

```sql
select pg_is_wal_replay_paused();
```

```sql
select pg_current_wal_flush_lsn();
```

```sql
select pg_drop_replication_slot('<replication-slot-name>');
```
