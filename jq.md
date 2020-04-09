# jq

This is my cheatsheet for anything related to `jq`

Manual: https://stedolan.github.io/jq/manual/

Every question is about JSON! :)

* How do I prettify json?

`jq` by default prettifies any json that it processes :)

```bash
$ echo '{"someKey": "someValue"}' | jq .
{
  "someKey": "someValue"
}

$ cat dummy.json
{"someKey": "someValue"}

$ cat dummy.json | jq
{
  "someKey": "someValue"
}

$ jq . dummy.json
{
  "someKey": "someValue"
}
```

* How do make I a json compact - with no spaces and new lines? like reverse of
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

* How do I find the value of a key which has a primitive value?

* How do I find the value of a key which is present in a nested object?

* How do I find the value of key which has array value?

* How do I filter in array based on a condition?

* How do I reverse a filter used for an array?

* How to join multiple JSON objects into an array?

* How to form custom JSON as output?

* How to do string interpolation?

Let's say we have a JSON and now we want to output some text or put
some text in a field using string interpolation - static string along
with the value of some variables. Let's see how to do just that

```
$ cat dummy.json
[{"name":"Karuppiah","age":25},{"name":"Joseph","age":29},{"name":"Kevin","age":30}]
```

Let's say we want to now form another JSON like this -

```
[
  {
    "text": "name is Karuppiah and their age is 25"
  },
  {
    "text": "name is Joseph and their age is 29"
  },
  {
    "text": "name is Kevin and their age is 30"
  }
]
```

As you can see how the text has the values of the variables. We can get such
an output with this command -

```
$ cat dummy.json | jq '.[] | { "text": "name is \(.name) and their age is \(.age)" }' | jq -s
```

A string is created using double quotes `""` and the interpolation - putting values
of variables / keys - is done using `\()` and by putting the key path in it referring to
the value present in the JSON. You can also do something like below and get a complete
text output -

```
$ cat dummy.json | jq '.[] | "name is \(.name) and their age is \(.age)"' -r
name is Karuppiah and their age is 25
name is Joseph and their age is 29
name is Kevin and their age is 30
```

* How to form custom text as output?

Check string interpolation answer which covers this too!

* How to output the raw value, instead of it being wrapped in double quotes
as a string?

Use `-r` or `--raw-output` flag. Example

```
$ cat dummy.json
[{"name":"Karuppiah","age":25},{"name":"Joseph","age":29},{"name":"Kevin","age":30}]

$ cat dummy.json | jq '.[] | .name'
"Karuppiah"
"Joseph"
"Kevin"

$ # with -r, you can get raw output!
$ cat dummy.json | jq '.[] | .name' -r
Karuppiah
Joseph
Kevin
```

* How to do a mapping using one array, to form another array?

* How to do a flat map (map with filter) using one array, to form another array?

