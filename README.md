# Website MULTIPLE certificates by Zabbix agent 2

Inspired by the original single certificate monitoring template, but much cooler:
We need a macro called `{$MULTICERT.CONFIG}` configuring the entire certificate monitoring in the following way, in one string:

```
HOSTNAME,<PORT>,<ADDRESS>;HOSTNAME,<PORT>,<ADDRESS>;...
```

This way, we can monitor as many certificates as we want, on one single host with one single template.

A "script" item (embedded ECMAScript5 JavaScript) will run to convert this Macro into a JSON structure that looks as follows:

[
  {"hostname":"host1.mycompany.com","port":"","address":""},
  {"hostname":"host2.mycompany.com","port":"443","address":"127.0.0.1"}
]

In case "port" or "address" is not needed, it can be omitted, also, in the Macro, double comma syntax can be used if only "hostname" and "address" is to be supplied.

From the above JSON structure, a Low Level Discovery will run and create 14 items and corresponding Triggers for each certificate.
