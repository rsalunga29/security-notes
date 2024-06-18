Zeek has its own event-driven scripting language, which allows defenders to investigate and correlate the detected events. This scripting language is as powerful as high-level languages and requires some time for someone to be proficient. Zeek scripts use the `.zeek` extension.

Zeek scripts are event-oriented, not packet oriented. It shall only be used to handle the event of interest.

Scripts can also be used to apply policies, in which case they are called "policy scripts".

Scripts can be called in live monitoring mode. This can be done by loading them with the command `load @/script/path` or `load @script-name` in `local.zeek` file.
## Script Locations
|                                                                                                                                                                                                          |                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| Zeek has base scripts installed by default, and these are not intended to be modified.                                                                                                                   | These scripts are located in "/opt/zeek/share/zeek/base".          |
| User-generated or modified scripts should be located in a specific path.                                                                                                                                 | These scripts are located in  <br>**"/opt/zeek/share/zeek/site".** |
| Policy scripts are located in a specific path.                                                                                                                                                           | These scripts are located in **"/opt/zeek/share/zeek/policy"**.    |
| Like Snort, to automatically load/use a script in live sniffing mode, you must identify the script in the Zeek configuration file. You can also use a script for a single run, just like the signatures. |                                                                    |