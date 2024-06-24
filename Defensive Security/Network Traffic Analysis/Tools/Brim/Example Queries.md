The following example queries can be used for threat hunting with Brim.
## View the Frequently Communicated Hosts
```txt
_path == "conn" | cut id.orig_h, id.resp_p, id.resp_h | sort  | uniq -c | sort -r count
```
## View Port Numbers and Services
```txt
_path == "conn" | cut id.resp_p, service | sort | uniq -c | sort -r count
```
## View All DNS Records
```txt
_path == "dns" | count() by query | sort -r
```
## View Host and URI from a specific IP Address
```txt
_path == "http" | cut host, uri | uniq -c | [IP_ADDRESS]
```
## Get Total Count of Connections Using a Specific Port
```txt
_path == "conn" id.resp_h == [IP_ADDRESS] id.resp_p == [PORT] | count() by id.resp_p
```
## Get Service of a Specific Port
```txt
_path == "conn" id.resp_p == [PORT] | cut service | uniq
```
## Get the Total Bytes Sent and Received by a Specific IP Address and Port
```txt
_path == "conn" | put total_bytes := orig_bytes + resp_bytes | [IP_ADDRESS] | [PORT] | cut uid, id, orig_bytes, resp_bytes, total_bytes
```