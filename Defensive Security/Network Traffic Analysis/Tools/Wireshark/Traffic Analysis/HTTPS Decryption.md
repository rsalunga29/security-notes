HTTPS uses TLS protocol to encrypt communications, so it is impossible to decrypt the traffic and view the transferred data without having the encryption/decryption key pairs.

| Notes                                                                                                                                                                                                                                                                                                                                                        | Wireshark Filter                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| "HTTPS Parameters" for grabbing the low-hanging fruits:<br><br>- **Request:** Listing all requests  <br>    <br>- **TLS:** Global TLS search<br>- TLS Client Request<br>- TLS Server response<br>- Local Simple Service Discovery Protocol (SSDP)<br><br>**Note:** SSDP is a network protocol that provides advertisement and discovery of network services. | - `http.request`<br><br>- `tls`<br><br>- `tls.handshake.type == 1`<br><br>- `tls.handshake.type == 2`<br><br>- `ssdp` |
Similar to the TCP three-way handshake process, the TLS protocol has its handshake process. The first two steps contain "Client Hello" and "Server Hello" messages. We can use the following to filter:
- **Client Hello**: `(http.request or tls.handshake.type == 1) and !(ssdp)` 
- **Server Hello**: `(http.request or tls.handshake.type == 2) and !(ssdp)`
## Saving and Utilizing an Encryption Key Log File
An encryption key log file is a text file that contains unique key pairs to decrypt the encrypted traffic session. These key pairs are automatically created (per session) when a connection is established with an SSL/TLS-enabled webpage.

To save the values of these key pairs as key log files, we need to use a suitable browser such as Chrome and Firefox.

Note: SSL/TLS key pairs are created per session at the connection time, so it is important to dump the keys during the traffic capture.

To save and utilize a key log file. Follow the following steps:
1. Setup an environment variable named "SSLKEYLOGFILE".
2. Create a file named SSLKEYLOGFILE (this is where the browser will dump the keys as you browse the web).
3. Go to the "Edit --> Preferences --> Protocols --> TLS" menu to add/remove key log files.