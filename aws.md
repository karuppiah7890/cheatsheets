# AWS

This is my cheatsheet for anything related to AWS

- List all users

```bash
aws iam list-users
```

- Store username and user id data in a JSON file

```bash
aws iam list-users --query "Users[*].{username: UserName, userid: UserId}" > users.json
```

- List all the access keys created by all the users

```bash
aws iam list-users --query "Users[*].{username: UserName, userid: UserId}" > users.json
```

```bash
cat users.json | jq '.[].username' -r | xargs -I{} aws iam list-access-keys --user-name {} | jq -s 
```
