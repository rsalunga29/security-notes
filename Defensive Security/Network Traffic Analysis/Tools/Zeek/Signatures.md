Zeek uses signatures to have rules and event correlations to find noteworthy activities on the network. Zeek signatures use low-level pattern matching and cover conditions similar to [Snort rules](obsidian://open?vault=security-notes&file=Defensive%20Security%2FNetwork%20Traffic%20Analysis%2FTools%2FSnort%2FRules). However, unlike Snort rules, Zeek rules are not the primary event detection point.

Zeek signatures supports regex and uses the `.sig` extension.

Zeek has a scripting language and can chain multiple events to find an event of interest.

Zeek signature files can consist of multiple signatures. Therefore we can have one file for each protocol/situation/threat type.
## Format
Zeek signatures are composed of three logical paths:

| Path         | Description                                                                                                                                                                                         |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Signature ID | Unique signature name.                                                                                                                                                                              |
| Conditions   | **Header:** Filtering the packet headers for specific source and destination addresses, protocol and port numbers.<br><br>**Content:** Filtering the packet payload for specific value/pattern.<br> |
| Action       | **Default action:** Create the "signatures.log" file in case of a signature match.<br><br>**Additional action:** Trigger a Zeek script.                                                             |
## Conditions and Filters
Below are the most common conditions and filters used for Zeek signatures:

| Condition Field               | Available Filters                                                                                                                                                                                                                                                                                                                                                |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Header                        | src-ip: Source IP.<br><br>dst-ip: Destination IP.<br><br>src-port: Source port.<br><br>dst-port: Destination port.<br><br>ip-proto: Target protocol. Supported protocols; TCP, UDP, ICMP, ICMP6, IP, IP6                                                                                                                                                         |
| Content                       | **payload:** Packet payload.  <br>**http-request:** Decoded HTTP requests.  <br>**http-request-header:** Client-side HTTP headers.  <br>**http-request-body:** Client-side HTTP request bodys.  <br>**http-reply-header:** Server-side HTTP headers.  <br>**http-reply-body:** Server-side HTTP request bodys.  <br>**ftp:** Command line input of FTP sessions. |
| **Context**                   | **same-ip:** Filtering the source and destination addresses for duplication.                                                                                                                                                                                                                                                                                     |
| Action                        | **event:** Signature match message.                                                                                                                                                                                                                                                                                                                              |
| **Comparison  <br>Operators** | **==**, **!=**, **<**, **<=**, **>**, **>=**                                                                                                                                                                                                                                                                                                                     |
| **NOTE!**                     | Filters accept string, numeric and regex values.                                                                                                                                                                                                                                                                                                                 |
## Examples
## Cleartext Submission of Password
```sig
signature http-password {
     ip-proto == tcp
     dst-port == 80
     payload /.*password.*/
     event "Cleartext Password Found!"
}
```
### FTP Brute Force
```sig
signature ftp-username {
	ip-proto == tcp
	ftp /.*USER.*/
    event "FTP Username Input Found!"
}

signature ftp-brute {
	ip-proto == tcp
	payload /.*530.*Login.*incorrect.*/
    event "FTP Brute-force Attempt"
}
```