# Syslog parsing

You may add the `syslog` section to the osquery-sender `config.yaml` file. For example:

```yaml
insecure: true
key: test_key
cert: test_cert
enrollment_hmac_secret: test_hmac_secret
hosts:
  localhost:8008:
    insecure_enroll: true
    url: http://localhost:9090/test
    token: test_splunk_token
    enroll_secret: test_splunk_enroll
syslog:
  servers:
    - name: JuniperStructured
      address: :5001
      parser: JuniperStructured
    - name: JuniperStandard
      address: :5002
      parser: JuniperStandard
    - name: Huawei
      address: :5003
      parser: Huawei
    - name: Cumulus
      address: :5004
      parser: Cumulus
    - name: Shell
      address: :5005
      parser: Shell
```

In this example, several syslog parser servers will be started. For every server, we specify:

- `name` : this value is a free text that will be set to `ParsedEvent.Name`, for every generated event
- `address` : here you can specify the port where the server listens
- `parser` : type of parser used to process the logs, see more info below

## Parsers

These are the available parsers.
You can see log examples in their corresponding tests.
- [Cumulus](parsers/cumulus.go) ([tests](parsers/cumulus_test.go))
- [Huawei](parsers/huawei.go) ([tests](parsers/huawei_test.go))
- [JuniperStandard](parsers/juniper_standard.go) ([tests](parsers/juniper_standard_test.go))
- [JuniperStructured](parsers/juniper_structured.go) ([tests](parsers/juniper_structured_test.go))
- [Shell](parsers/shell.go) ([tests](parsers/shell_test.go))
- `printLogLine` : prints the log line, see about debugging later
- `printLogParts` : prints the parsed log parts, see about debugging later

## Debugging

To investigate logs, you have some debugging options.
These examples might be useful:

```yaml
syslog:
  servers:
    - name: Print Logs
      address: :5001
      parser: printLogLine
      event_handler: IgnoreEvent
    - name: Check Shell Events
      address: :5002
      parser: Shell
      event_handler: PrintEvent
```

In `Print Logs`, we don't parse the logs, we just print them. Use this when you don't know the format of the logs, and you just want to see how they look like.
Note that we use the especial handler `IgnoreEvent` because the dummy parser `printLogLine` doesn't generate any meaningful events.

In `Check Shell Events`, we parse the logs with the `Shell` parser, but we don't send the generated events, we just log their content. Use this to check that the parsed events are being generated correctly.
Note that we use `PrintEvent` because the `Shell` parser creates events, so it makes sense to print them to see how they look like.

These debugging options could be improved in [syslogparsing.go](syslogparsing.go), if necessary.
