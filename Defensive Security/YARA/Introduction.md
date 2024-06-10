YARA is a tool primarily used for malware identification and detection. With YARA, malware researchers can create descriptions of malware families based on textual or binary patterns, such as hexadecimal and strings contained within the malicious file. To accomplish this, YARA uses rules to label these patterns.
## Why does Malware use Strings?
Malware, just like any other application, uses strings to store textual data. Here are a few examples of the data that various malware types store within strings:

| **Type**   | **Data**                                                                                                        | **Description**                                        |
| ---------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| Ransomware | [12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw](https://www.blockchain.com/btc/address/12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw) | Bitcoin Wallet for ransom payments                     |
| Botnet     | 12.34.56.7                                                                                                      | The IP address of the Command and Control (C&C) server |
