## Packet Filter Toolbar
Wireshark's filter toolbar is where filters are created and applied. It is a smart toolbar that helps to create valid filters. It uses a three-color representation based on the validity of the filter:
- **Green**: Valid Filter
- **Red**: Invalid Filter
- **Yellow**: Warning Filter. The filter works but is unreliable.
## Comparison Operators

| **English** | **C-Like** | **Description**          | **Example**              |
| ----------- | ---------- | ------------------------ | ------------------------ |
| eq          | ==         | Equal                    | `ip.src == 10.10.10.100` |
| ne          | !=         | Not equal                | `ip.src != 10.10.10.100` |
| gt          | >          | Greater than             | `ip.ttl > 250`           |
| lt          | <          | Less Than                | `ip.ttl < 10`            |
| ge          | >=         | Greater than or equal to | `ip.ttl >= 0xFA`         |
| le          | <=         | Less than or equal to    | `ip.ttl <= 0xA`          |
## Logical Expressions

| **English** | **C-Like** | **Description** | **Example**                                                                                           |
| ----------- | ---------- | --------------- | ----------------------------------------------------------------------------------------------------- |
| and         | &&         | Logical AND     | `(ip.src == 10.10.10.100) AND (ip.src == 10.10.10.111)`                                               |
| or          | \|         | Logical OR      | `(ip.src == 10.10.10.100) OR (ip.src == 10.10.10.111)`                                                |
| not         | !          | Logical NOT     | `!(ip.src == 10.10.10.222)`<br><br>**Note:** Usage of `!=value` is deprecated; Use `!(value)` instead |
## Protocol Filters
### Ethernet Filters
| Filter                          | Description                                                     |
| ------------------------------- | --------------------------------------------------------------- |
| `eth`                           | Show all ethernet packets.                                      |
| `eth.addr == 08:00:08:15:ca:fe` | Show all packets containing ethernet address 08:00:08:15:ca:fe. |
| `eth.src == 08:00:08:15:ca:fe`  | Show all packets originated from 08:00:08:15:ca:fe              |
| `eth.dst == 08:00:08:15:ca:fe`  | Show all packets sent to 08:00:08:15:ca:fe                      |
### IP Filters

| Filter                     | Description                                                         |
| -------------------------- | ------------------------------------------------------------------- |
| `ip`                       | Show all IP packets.                                                |
| `ip.addr == 10.10.10.111`  | Show all packets containing IP address 10.10.10.111.                |
| `ip.addr == 10.10.10.0/24` | Show all packets containing IP addresses from 10.10.10.0/24 subnet. |
| `ip.src == 10.10.10.111`   | Show all packets originated from 10.10.10.111                       |
| `ip.dst == 10.10.10.111`   | Show all packets sent to 10.10.10.111                               |
### TCP and UDP Filters

| Filter                | Description                                     | Filter                | Expression                                      |
| --------------------- | ----------------------------------------------- | --------------------- | ----------------------------------------------- |
| `tcp.port == 80`      | Show all TCP packets with port 80               | `udp.port == 53`      | Show all UDP packets with port 53               |
| `tcp.srcport == 1234` | Show all TCP packets originating from port 1234 | `udp.srcport == 1234` | Show all UDP packets originating from port 1234 |
| `tcp.dstport == 80`   | Show all TCP packets sent to port 80            | `udp.dstport == 5353` | Show all UDP packets sent to port 5353          |
### HTTP and DNS Filters

| Filter                          | Description                                    | Filter                    | Description              |
| ------------------------------- | ---------------------------------------------- | ------------------------- | ------------------------ |
| `http`                          | Show all HTTP packets                          | `dns`                     | Show all DNS packets     |
| `http.response.code == 200`     | Show all packets with HTTP response code "200" | `dns.flags.response == 0` | Show all DNS requests    |
| `http.request.method == "GET"`  | Show all HTTP GET requests                     | `dns.flags.response == 1` | Show all DNS responses   |
| `http.request.method == "POST"` | Show all HTTP POST requests                    | `dns.qry.type == 1`       | Show all DNS "A" records |
## Advanced Filters
### "contains" Filter
|                 |                                                                                                                                              |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Filter          | contains                                                                                                                                     |
| **Type**        | Comparison Operator                                                                                                                          |
| **Description** | Search a value inside packets. It is case-sensitive and provides similar functionality to the "Find" option by focusing on a specific field. |
| **Example**     | Find all "Apache" servers.                                                                                                                   |
| **Workflow**    | List all HTTP packets where packets' "server" field contains the "Apache" keyword.                                                           |
| **Usage**       | `http.server contains "Apache"`                                                                                                              |
### "matches" Filter
|             |                                                                                                               |
| ----------- | ------------------------------------------------------------------------------------------------------------- |
| Filter      | matches                                                                                                       |
| Type        | Comparison Operator                                                                                           |
| Description | Search a pattern of a regular expression. It is case insensitive, and complex queries have a margin of error. |
| **Example** | Find all .php and .html pages.                                                                                |
| Workflow    | List all HTTP packets where packets' "host" fields match keywords ".php" or ".html".                          |
| **Usage**   | `http.host matches "\.(php\|html)"`                                                                           |
### "in" Filter
|             |                                                                                |
| ----------- | ------------------------------------------------------------------------------ |
| Filter      | in                                                                             |
| Type        | Set Membership                                                                 |
| Description | Search a value or field inside of a specific scope/range.                      |
| Example     | Find all packets that use ports 80, 443 or 8080.                               |
| Workflow    | List all TCP packets where packets' "port" fields have values 80, 443 or 8080. |
| Usage       | `tcp.port in {80 443 8080}`                                                    |
Another Example:

|          |                                                                                     |
| -------- | ----------------------------------------------------------------------------------- |
| Example  | Find all packets that use ports between 8001 to 9001.                               |
| Workflow | List all TCP packets where packets' "port" fields have values between 8001 to 9001. |
| Usage    | `tcp.port in {8001 .. 9001}`                                                        |
### "upper" Filter
|             |                                                                                                            |
| ----------- | ---------------------------------------------------------------------------------------------------------- |
| Filter      | upper                                                                                                      |
| Type        | Function                                                                                                   |
| Description | Convert a string value to uppercase.                                                                       |
| Example     | Find all "APACHE" servers.                                                                                 |
| Workflow    | Convert all HTTP packets' "server" fields to uppercase and list packets that contain the "APACHE" keyword. |
| Usage       | `upper(http.server) contains "APACHE"`                                                                     |
### "lower" Filter
|             |                                                                                                                 |
| ----------- | --------------------------------------------------------------------------------------------------------------- |
| Filter      | lower                                                                                                           |
| Type        | Function                                                                                                        |
| Description | Convert a string value to lowercase.                                                                            |
| Example     | Find all "apache" servers.                                                                                      |
| Workflow    | Convert all HTTP packets' "server" fields info to lowercase and list packets that contain the "apache" keyword. |
| **Usage**   | `lower(http.server) contains "apache"`                                                                          |
### "string" Filter
|             |                                                                                          |
| ----------- | ---------------------------------------------------------------------------------------- |
| Filter      | string                                                                                   |
| Type        | Function                                                                                 |
| Description | Convert a non-string value to a string.                                                  |
| Example     | Find all frames with odd numbers.                                                        |
| Workflow    | Convert all "frame number" fields to string values, and list frames end with odd values. |
| Usage       | `string(frame.number) matches "[13579]$"`                                                |