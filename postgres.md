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