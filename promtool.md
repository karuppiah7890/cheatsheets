# promtool

This is my cheatsheet for anything related to `promtool`

* How to run an instant query against prometheus?

```
$ promtool query instant <prometheus-url> <expression>
```

Example:

```
$ promtool query instant http://localhost:9090 'container_memory_working_set_bytes{name=~".*redis.*"}'
```

* How to change the output format of the output?

By default the format is `promql`. Usually the command has `--format` or `-o`
flag to change the output format. The only possible values as of this writing
are `promql` and `json`
