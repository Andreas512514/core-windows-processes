# core-windows-processes

 We will explore the core processes within a Windows system.

 ![Task manager screenshot](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-21%20225413.png)

You can open the Process Explorer program. You can download from [here](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer).<br><br>

You can also open the Process Hacker program.

![process hacker](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-21%20231426.png)<br><br><br>


## System

The System process (process ID 4) is the home for a special kind of thread that runs only in kernel mode a kernel-mode system thread.<br><br>

![Screenshot process systme](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-21%20232429.png)

**Image Path:**  N/A<br>
**Parent Process:**  None<br>
**Start Time:**  At boot time<br><br>

The information in **Process Hacker** in a little different.

![screenshot process system(process hacker)](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-21%20232346.png)

**Image Path:** C:\Windows\system32\ntoskrnl.exe (NT OS Kernel)<br>
**Parent Process:** System Idle Process (0)

**Remember** that the PID will always be PID 4 and should only be one instance.<br><br><br>


## System > smss.exe (Session Manager Subsystem)


