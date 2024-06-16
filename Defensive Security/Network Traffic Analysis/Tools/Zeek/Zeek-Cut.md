The `zeek-cut` is an auxiliary program to help reduce the effort of extracting specific columns from log files. For example:
```bash
cat conn.log | zeek-cut uid proto id.orig_h id.orig_p id.resp_h id.resp_p
```
The command above extracts the uid, protocol, source and destination hosts, and source and destination ports.