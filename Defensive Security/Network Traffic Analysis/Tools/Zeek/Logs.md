Zeek generate log files according to the traffic data. Zeek is capable of identifying 50+ logs and categorizing them into seven categories.

Zeek logs are well structured and tab-separated ASCII files, making it easy to read and process them, but still requires effort. Investigating these logs will require the help of additional command-line tools (i.e cat)

Each log output consists of multiple fields, and each field holds a different part of the traffic data. Correlation is done through a unique value called "UID". The "UID" represents the unique identifier assigned to each session.
## Logs Category

| Category             | Description                                                              | **Log Files**                                                                                                                                                                                                                                                                                                                      |
| -------------------- | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Network              | Network protocol logs.                                                   | _conn.log, dce_rpc.log, dhcp.log, dnp3.log, dns.log, ftp.log, http.log, irc.log, kerberos.log, modbus.log, modbus_register_change.log, mysql.log, ntlm.log, ntp.log, radius.log, rdp.log, rfb.log, sip.log, smb_cmd.log, smb_files.log, smb_mapping.log, smtp.log, snmp.log, socks.log, ssh.log, ssl.log, syslog.log, tunnel.log._ |
| Files                | File analysis result logs.                                               | _files.log, ocsp.log, pe.log, x509.log._                                                                                                                                                                                                                                                                                           |
| NetControl           | Network control and flow logs.                                           | _netcontrol.log, netcontrol_drop.log, netcontrol_shunt.log, netcontrol_catch_release.log, openflow.log._                                                                                                                                                                                                                           |
| Detection            | Detection and possible indicator logs.                                   | _intel.log, notice.log, notice_alarm.log, signatures.log, traceroute.log._                                                                                                                                                                                                                                                         |
| Network Observations | Network flow logs.                                                       | _known_certs.log, known_hosts.log, known_modbus.log, known_services.log, software.log._                                                                                                                                                                                                                                            |
| Miscellaneous        | Additional logs cover external alerts, inputs and failures.              | _barnyard2.log, dpd.log, unified2.log, unknown_protocols.log, weird.log, weird_stats.log._                                                                                                                                                                                                                                         |
| Zeek Diagnostic      | Zeek diagnostic logs cover system messages, actions and some statistics. | _broker.log, capture_loss.log, cluster.log, config.log, loaded_scripts.log, packet_filter.log, print.log, prof.log, reporter.log, stats.log, stderr.log, stdout.log._                                                                                                                                                              |
### Investigation Matrix Example
Categorizing the logs before starting an investigation makes it easier for you to find the evidence/anomaly you are looking for. The table below is an example of creating a working matrix/model of multiple log files to help you create correlations.

| **Overall Info**     | **Protocol Based** | **Detection**    | **Observation**      |
| -------------------- | ------------------ | ---------------- | -------------------- |
| _conn.log_           | _http.log_         | _notice.log_     | _known_host.log_     |
| _files.log_          | _dns.log_          | _signatures.log_ | _known_services.log_ |
| _intel.log_          | _ftp.log_          | _pe.log_         | _software.log_       |
| _loaded_scripts.log_ | _ssh.log_          | _traceroute.log_ | _weird.log_          |
- **Overall Info:** The aim is to review the overall connections, shared files, loaded scripts and indicators at once. This is the first step of the investigation.
- **Protocol Based:** Once you review the overall traffic and find suspicious indicators or want to conduct a more in-depth investigation, you focus on a specific protocol.
- **Detection:** Use the prebuild or custom scripts and signature outcomes to support your findings by having additional indicators or linked actions. 
- **Observation:** The summary of the hosts, services, software, and unexpected activity statistics will help you discover possible missing points and conclude the investigation.
## Logs Update Frequency
Although there are multiple log files, some log files are updated daily, and some are updated in each session.

| **Update Frequency** | **Log Name  <br>**   | **Description**                                 |
| -------------------- | -------------------- | ----------------------------------------------- |
| **Daily**            | _known_hosts.log_    | List of hosts that completed TCP handshakes.    |
| **Daily**            | _known_services.log_ | List of services used by hosts.                 |
| **Daily**            | _known_certs.log_    | List of SSL certificates.                       |
| **Daily**            | _software.log_       | List of software used on the network.           |
| **Per Session**      | _notice.log_         | Anomalies detected by Zeek.                     |
| **Per Session**      | _intel.log_          | Traffic contains malicious patterns/indicators. |
| Per Session          | _signatures.log_     | List of triggered signatures.                   |
