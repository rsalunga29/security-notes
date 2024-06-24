The following example queries can be used for threat hunting with Brim.
## View the Frequently Communicated Hosts
```txt
_path == "conn" | cut id.orig_h, id.resp_p, id.resp_h | sort  | uniq -c | sort -r count
```
## View Port Numbers and Services
```txt
_path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count
```