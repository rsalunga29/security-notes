## Package Manager
Zeek Package Manager helps users install third-party scripts and plugins to extend Zeek functionalities with ease. The package manager is installed with Zeek and available with the `zkg` command.

The following is the basic usage of the `zkg` command:

| **Command**                | **Description**                                                             |
| -------------------------- | --------------------------------------------------------------------------- |
| `zkg install package_path` | Install a package. Example (zkg install zeek/j-gras/zeek-af_packet-plugin). |
| `zkg install git_url`      | Install package. Example (zkg install https://github.com/corelight/ztest).  |
| `zkg list`                 | List installed package.                                                     |
| `zkg remove`               | Remove installed package.                                                   |
| `zkg refresh`              | Check version updates for installed packages.                               |
| `zkg upgrade`              | Update installed packages.                                                  |
## Using Packages
There are multiple ways of using packages:
The first approach is using them as frameworks and calling specific package path/directory or package name per usage. For example:
```bash
zeek -C -r http.pcap /opt/zeek/share/zeek/site/zeek-sniffpass
```
```bash
zeek -C -r http.pcap zeek-sniffpass
```

The second and most common approach is calling packages from a script with the `@load` method. For example:
```zeek
# File Name: sniff-demo.zeek
@load /opt/zeek/share/zeek/site/zeek-sniffpass
```
```bash
zeek -C -r http.pcap sniff-demo.zeek
```