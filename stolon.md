# Stolon

This is my cheatsheet for anything related to GitLab

1. How do I connect to my Postgres server of a Stolon cluster?

If you have used environment variables to start your stolon keeper, you can
get into your keeper instance and run this

```bash
$ PGPASSWORD=$(cat $STKEEPER_PG_SU_PASSWORDFILE) psql -h localhost -U $STKEEPER_PG_SU_USERNAME postgres
```
