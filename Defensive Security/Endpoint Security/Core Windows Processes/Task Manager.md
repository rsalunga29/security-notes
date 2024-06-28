Task Manager is a built-in GUI-based Windows utility that allows users to see what is running on the Windows system. It also provides information on resource usage, such as how much each process utilizes CPU and memory. When a program is not responding, Task Manager is used to end (kill) the process.

By default, the columns **Name**, **Status**, **CPU**, and **Memory** are the only ones visible. To view more columns, right-click on any column header to open more options.

In the Details tab, the **Image Path Name** and **Command Line** are some good columns to add. These two columns can quickly alert an analyst of any outliers with a given process.

Aside from Task Manager, it would be best if you also familiarize yourself with the command-line equivalent of obtaining information about the running processes on a Windows system: `tasklist`, `Get-Process` or `ps` (PowerShell), and `wmic`.
## Process Hacker and Explorer
Task Manager only gives limited details about the processes that are running. To obtain more information, the Process Hacker and Process Explorer software can be used.