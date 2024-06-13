Once Snort is installed, the required directories and files are automatically created. However, if community or paid rules needs to be used, each rule needs to be indicated in the `snort.conf` file.

- snort.conf: _Main configuration file._
- local.rules: _User-generated rules file._
## Config Modification
Editing the `snort.conf` is usually troublesome due to it being an all-in-one configuration file. It's important to never replace the original Snort configuration file. Instead, a backup must be created first, and the configuration files must be edited manually or rules updated using additional tools or modules to not face any fail/crash or lack of feature.

The "**Step #1: Set the network variables.**" section of the config file manages the scope of the detection and rule paths. It contains the following variables:

| **TAG NAME**      | **INFO**                                                                            | **EXAMPLE**               |
| ----------------- | ----------------------------------------------------------------------------------- | ------------------------- |
| HOME_NET          | That is where we are protecting.                                                    | 'any' OR '192.168.1.1/24' |
| EXTERNAL_NET      | This field is the external network, so we need to keep it as 'any' or '!$HOME_NET'. | 'any' OR '!$HOME_NET'     |
| RULE_PATH         | Hardcoded rule path.                                                                | /etc/snort/rules          |
| SO_RULE_PATH      | _These rules come with registered and subscriber rules._                            | $RULE_PATH/so_rules       |
| PREPROC_RULE_PATH | _These rules come with registered and subscriber rules._                            | $RULE_PATH/plugin_rules   |
The "**Step #2: Configure the decoder.**" section manages the IPS mode. The single-node installation model of the IPS model works best with the `afpacket` mode, which can be enabled to run Snort in IPS mode. It contains the following variables:

| **TAG NAME**       | **INFO**                    | **EXAMPLE**     |
| ------------------ | --------------------------- | --------------- |
| # config daq:      | IPS mode selection.         | afpacket        |
| # config daq_mode: | Activating the inline mode  | inline          |
| # config logdir:   | Hardcoded default log path. | /var/logs/snort |
DAQ or Data Acquisition Modules are specific libraries used for packet I/O, bringing flexibility to process packets. It is possible to select DAQ type and mode for different purposes.

There are six DAQ modules available in Snort;
- **Pcap:** Default mode, known as Sniffer mode. One of the most popular modes.
- **Afpacket:** Inline mode, known as IPS mode. The other popular mode.
- **Ipq:** Inline mode on Linux by using Netfilter. It replaces the snort_inline patch.  
- **Nfq:** Inline mode on Linux.
- **Ipfw:** Inline on OpenBSD and FreeBSD by using divert sockets, with the pf and ipfw firewalls.  
- **Dump:** Testing mode of inline and normalization.

The "**Step #6: Configure output plugins**" section manages the outputs of the IDS/IPS modes, such as logging and alerting format details.

The "**Step #7: Customize your ruleset**" section manages the rules that Snort will use. It contains the following variables:

| **TAG NAME**              | **INFO**                                       | **EXAMPLE**                    |
| ------------------------- | ---------------------------------------------- | ------------------------------ |
| **# site specific rules** | Hardcoded local and user-generated rules path. | include $RULE_PATH/local.rules |
| **# include $RULE_PATH/** | Hardcoded default/downloaded rules path.       | include $RULE_PATH/rulename    |
