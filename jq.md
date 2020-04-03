# jq

This is my cheatsheet for anything related to `jq`

Manual: https://stedolan.github.io/jq/manual/

Every question is about JSON! :)

1. How do I prettify json?

`jq` by default prettifies any json that it processes :)

```bash
$ echo '{ "someKey": "someValue" }' | jq .
{
  "someKey": "someValue"
}

$ cat dummy.json
{ "someKey": "someValue" }

$ cat dummy.json | jq
{
  "someKey": "someValue"
}

$ jq . dummy.json
{
  "someKey": "someValue"
}
```

2. How do make I a json compact - with no spaces and new lines? like reverse of
prettify

```
$ cat dummy.json
{
  "someKey": "someValue"
}

$ cat dummy.json | jq -c
{"someKey":"someValue"}

$ jq -c . dummy.json
{"someKey":"someValue"}

$ # option can come later too!
$ jq . dummy.json -c
{"someKey":"someValue"}

```

3. How do I find the value of a key which has a primitive value?

4. How do I find the value of a key which is present in a nested object?

5. How do I find the value of key which has array value?

6. How do I filter in array based on a condition?

7. How do I reverse a filter used for an array?

How to join multiple JSON objects into an array?

How to form custom JSON as output?

How to do string interpolation?

How to form custom text as output?

How to output the raw value, instead of it being wrapped in double quotes
as a string?

How to do a mapping using one array, to form another array?

How to do a flat map (map with filter) using one array, to form another array?

