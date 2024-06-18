Scripts contain operators, types, attributes, declarations and statements, and directives.
## Init and Done
The simple events `zeek_init` and `zeek_done` works once the Zeek process starts or stops. While these events doesn't have parameters, some events will require parameters.
```zeek
event zeek_init()
{
	print("Started Zeek!");
}

event zeek_done()
{
	print("Stopped Zeek!");
}
```
## Events with Parameters
In this following script, we are requesting details of a connection and extracting them without any filtering or sorting of the data.
```zeek
event new_connection(c: connection)
{
	print("New Connection Found!");
	print fmt("Source Host: %s # %s --->", c$id$orig_h, $c)
	
}
```