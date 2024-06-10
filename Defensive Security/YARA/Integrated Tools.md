There are plenty of GitHub [resources](https://github.com/InQuest/awesome-yara) and open-source tools (along with commercial products) that can be utilized to leverage Yara in hunt operations and/or incident response engagements.
## LOKI
LOKI is a free open-source IOC (_Indicator of Compromise_) scanner created/written by Florian Roth. LOKI can be used on both Windows and Linux systems.
## THOR
THOR _Lite_ is Florian's newest multi-platform IOC AND YARA scanner. There are precompiled versions for Windows, Linux, and macOS. A nice feature with THOR Lite is its scan throttling to limit exhausting CPU resources.
## FENRIR
This is the 3rd tool created by Florian Roth. The updated version was created to address the issue from its predecessors, where requirements must be met for them to function. Fenrir is a bash script; it will run on any system capable of running bash (nowadays even Windows).
## YAYA
Acronym for Yet Another Yara Scanner, is a tool created by the Electronic Frontier Foundation (EFF) and released in September 2020. It is an open-source tool to help researchers manage multiple YARA rule repositories.
## yarGen
This is another tool created by Florian Roth, it's meant to aid defenders in creating new Yara rules from strings found in malware files while removing all strings that also appear in goodware files. To generate a Yara rule, use the following command:
```bash
python3 yarGen.py -m /home/compromised/legit-file --excludegood -o /home/compromised/rule-legit-file.yar
```
## Valhalla
Valhalla is an online Yara feed created and hosted by [Nextron-Systems](https://www.nextron-systems.com/valhalla/). It's meant to boost a defender's detection capabilities with the power of thousands of hand-crafted high-quality YARA rules.