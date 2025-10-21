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

This process, also known as the **Windows Session Manager**, is responsible for creating new sessions. It is the first user-mode process started by the kernel.<br><br>

What is normal?

![smss.exe](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-22%20003356.png)

**Parent Process:**  System<br>
**Number of Instances:**  One master instance and child instance per session. The child instance exits after creating the session.<br>
**User Account:  Local System**<br>
**Start Time:**  Within seconds of boot time for the master instance<br>

What is unusual?

A different parent process other than System (4)<br>
The image path is different from C:\Windows\System32<br>
More than one running process. (children self-terminate and exit after each new session)<br>
The running User is not the SYSTEM user<br>
