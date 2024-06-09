Frameworks such as the [Cuckoo Sandbox](https://cuckoosandbox.org/) or [Python's PE Module](https://pypi.org/project/pefile/) allows defenders to improve their Yara rules ten-fold.
## Cuckoo
Cuckoo Sandbox is an automated malware analysis environment. This module will generate Yara rules based upon the behaviors discovered from the sandbox. As this environment executes the malware, defenders can create rules based on behavior, runtime strings, and the like.
## Python PE
This module allows to create Yara rules from the various sections and elements of the Windows Portable Executable (PE) structure.

Examining a PE file's contents is an essential technique in malware analysis; this is because behaviors such as cryptography or worming can be largely identified without reverse engineering or execution of the sample.