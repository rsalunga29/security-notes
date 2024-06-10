Snort can be ran with multiple combined parameters.
## Configuration Validity
```bash
snort -c /etc/snort/snort.conf -T
```
The `-c` parameter identifies the config file, while the `-T` is Snort's self-test parameter.
## Sniffer Mode: With Parameter "-i" and "-v"
```bash
snort -i eth0 -v
```
Starts the Snort instance in verbose mode (`-v`) and define the network interface to sniff/listen (`-i`).
## Sniffer Mode: With Parameter "-d" and "-e"
```bash
snort -d -e
```
Starts the Snort instance in dumping packet mode (`-d`) and link-layer header grabbing mode (`-e`).
## Sniffer Mode: With Parameter "-X"
```bash
snort -X
```
Starts the Snort instance in full packet dump mode (`-X`). This will also display the full packet details in HEX when reading logs. For example:
```bash
snort -r snort.log -X
```
## Packet Logger Mode: With Parameter "-l"
```bash
snort -dev -l .
```
Starts the Snort instance in packet logger mode and creates the logs in the current directory. The logs that are created requires specialize tools like `tcpdump` to be read.
## Packet Logger Mode: With Parameter "-K ASCII"
```bash
snort -dev -K ASCII -l .
```
Starts the Snort instance in packet logger mode and creates logs in ASCII format, which makes it human-readable without using a specialized tool.
## Packet Logger Mode: With Parameter "-r"
```bash
snort -r snort.log [icmp/tcp/udp]
```
Starts the Snort instance in packet reader mode (`-r`). Note that, logs created with the `-K ASCII` format parameter can't be read by this command. This command also allows the user to filter the log files. For example, if I want to see all TCP port 80 packets:
```bash
snort -r snort.log 'tcp and port 80'
```

The parameter `-n` can also be added to determine how many packets will be read. For example `-n 10` will process only the first 10 packets.
## IDS/IPS Mode: With Parameter "-N"
```bash
snort -c /etc/snort/snort.conf -N
```
Starts the Snort instance and disable logging (`-N`).
## IDS/IPS Mode: With Parameter "-D"
```bash
snort -c /etc/snort/snort.conf -D
```
Starts the Snort instance in background mode (`-D`).
## IDS/IPS Mode: With Parameter "-A"
```bash
snort -c /etc/snort/snort.conf -A [console/cmg/full/fast/none]
```
Starts the Snort instance in different alert modes:
- **console**: Provides fast style alerts on the console screen.
- **cmg**: Provides basic header details with payload in hex and text format.
- **full:** Full alert mode, providing all possible information about the alert.  
- **fast:** Fast mode, shows the alert message, timestamp, source and destination ıp along with port numbers.
- **none:** Disabling alerting.
## IDS/IPS Mode: Without Configuration File
It's possible to run Snort IDS/IPS mode without a configuration file. For example:
```bash
snort -c /etc/snort/rules/local.rules -A console
```
However, this will provide less performance, so this is mostly used for instances where we need to test user-created rules.
## IDS/IPS Mode: Activate IPS and Drop Packets
```bash
snort -c /etc/snort/snort.conf -Q --daq afpacket -i eth0:eth1 -A console
```