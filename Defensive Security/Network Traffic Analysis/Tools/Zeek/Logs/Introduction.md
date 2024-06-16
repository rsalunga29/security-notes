Zeek generate log files according to the traffic data. Zeek is capable of identifying 50+ logs and categorizing them into seven categories.

Zeek logs are well structured and tab-separated ASCII files, making it easy to read and process them, but still requires effort. Investigating these logs will require the help of additional command-line tools (i.e `cat`, `grep`, `uniq`) and additional tools (i.e [zeek-cut](obsidian://open?vault=security-notes&file=Defensive%20Security%2FNetwork%20Traffic%20Analysis%2FTools%2FZeek%2FZeek-Cut)).

Each log output consists of multiple fields, and each field holds a different part of the traffic data. Correlation is done through a unique value called "UID". The "UID" represents the unique identifier assigned to each session.