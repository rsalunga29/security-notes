Zeek scripts can also work with the [15+ frameworks](obsidian://open?vault=security-notes&file=Defensive%20Security%2FNetwork%20Traffic%20Analysis%2FTools%2FZeek%2FFrameworks) of Zeek to help analysts discover the different events of interest.

Not all framework functionalities are intended to be used in CLI mode. The majority of them are used in scripting.
## Loading Frameworks
You can easily load a framework in scripts by calling the specific framework in your Zeek script file. For example:
```zeek
# Enable MD5, SHA1 and SHA256 hashing for all files.
@load /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek
```

Another way of using a framework is to call it as parameter of a command. For example:
```bash
zeek -C -r sample.pcap /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek
```
## Some Examples
### File Framework - Hashes
This file framework will perform MD5 and SHA1 hashing on all files that are transferred, this will create a `files.log`.
```bash
zeek -C -r sample.pcap /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek
```
### File Framework - Extract Files
The file framework can extract the files transferred. A new folder called "extract_files" is automatically created, and all detected files are located in it.
```bash
zeek -C -r sample.pcap /opt/zeek/share/zeek/policy/frameworks/files/extract-all-files.zeek
```
### Notice Framework - Intelligence
The intelligence framework can work with data feeds to process and correlate events and identify anomalies. The intelligence framework requires a feed to match and create alerts from the network traffic.

The intelligence framework can work with data feeds to process and correlate events and identify anomalies. The intelligence framework requires a feed to match and create alerts from the network traffic.

Example of a Zeek intel file below:
```txt
#fields	indicator	indicator_type	meta.source	meta.desc
smart-fax.com	Intel::DOMAIN	zeek-intel-test	Zeek-Intel-Framework-Test
```