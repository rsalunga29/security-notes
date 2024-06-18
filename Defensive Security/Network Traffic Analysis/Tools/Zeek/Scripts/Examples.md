Scripts contain operators, types, attributes, declarations and statements, and directives.
## Init and Done
The simple events `zeek_init` and `zeek_done` works once the Zeek process starts or stops. While these events doesn't have parameters, some [events](https://docs.zeek.org/en/master/scripts/base/bif/event.bif.zeek.html) will require parameters.
```zeek
event zeek_init()
{
	print("Started Zeek!");
}

event zeek_done()
{
	print("Stopped Zeek!");
}

# zeek_init: Do actions once Zeek starts its process.
# zeek_done: Do activities once Zeek finishes its process.
# print: Prompt a message on the terminal.
```
## Events with Parameters
In this following script, we are requesting details of a connection and extracting them without any filtering or sorting of the data.
```zeek
event new_connection(c: connection)
{
	print("New Connection Found!");
	print fmt("Source Host: %s # %s --->", c$id$orig_h, c$id$orig_p);
	print fmt("Desination Host: %s # %s <---", c$id$resp_h, c$id$resp_p);
}

# %s: Identifies string output for the source.
# c$id: Source reference field for the identifier.
```

Another example, which tells Zeek to extract DHCP hostnames.
```zeek
event dhcp_message (c: connection, is_orig: bool, msg: DHCP::Msg, options: DHCP::Options)
{
	print options$host_name;
}
```
## Using Scripts and Signatures Together
Zeek scripts can refer to signatures and other Zeek scripts as well. This flexibility provides a massive advantage in event correlation.

The following script detects if the signature rule "ftp-admin" has a hit:
```zeek
event signature_match(state: signature_state, msg: string, data: string)
{
	if (state$sig_id == "ftp-admin") {
		print("Signature hit! --> #FTP-Admin");
	}
}
```
## Load Local Scripts
