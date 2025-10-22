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
**Start Time:**  Within seconds of boot time for the master instance<br><br>

What is unusual?

A different parent process other than System (4)<br>
The image path is different from C:\Windows\System32<br>
More than one running process. (children self-terminate and exit after each new session)<br>
The running User is not the SYSTEM user<br><br><br>


## csrss.exe

**csrss.exe** (**Client Server Runtime Process**) is the user-mode side of the Windows subsystem. This process is always running and is critical to system operation. If this process is terminated by chance, it will result in system failure. This process is responsible for the Win32 console window and process thread creation and deletion. For each instance, csrsrv.dll, basesrv.dll, and winsrv.dll are loaded (along with others).

This process is also responsible for making the Windows API available to other processes, mapping drive letters, and handling the Windows shutdown process.

csrss.exe and winlogon.exe are called from smss.exe at startup for Session 1. 

![csrss.exe proparties screenshoot](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-22%20235222.png)

What is normal

**Image Path:**  %SystemRoot%\System32\csrss.exe<br>
**Parent Process:**  Created by an instance of smss.exe<br>
**Number of Instances:**  Two or more<br>
**User Account:**  Local System<br>

What is unusual?

An actual parent process. (smss.exe calls this process and self-terminates)<br>
Image file path other than C:\Windows\System32<br>
Subtle misspellings to hide rogue processes masquerading as csrss.exe in plain sight<br>
The user is not the SYSTEM user.<br><br><br>



## wininit.exe

The **Windows Initialization Process**, **wininit.exe**, is responsible for launching services.exe (Service Control Manager), lsass.exe (Local Security Authority), and lsaiso.exe within Session 0. It is another critical Windows process that runs in the background, along with its child processes. 

![processes](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-23%20001041.png)

![wininit.exe screenshot](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-23%20001851.png)

What is normal?

**Image Path:**  %SystemRoot%\System32\wininit.exe<br>
**Parent Process:**  Created by an instance of smss.exe<br>
**Number of Instances:**  One<br>
**User Account:**  Local System<br>
**Start Time:**  Within seconds of boot time<br>

What is unusual?

An actual parent process. (smss.exe calls this process and self-terminates)<br>
Image file path other than C:\Windows\System32<br>
Subtle misspellings to hide rogue processes in plain sight<br>
Multiple running instances<br>
Not running as SYSTEM<br><br><br>


## wininit.exe > services.exe

The next process is the **Service Control Manager** (SCM) or **services.exe**. Its primary responsibility is to handle system services: loading services, interacting with services and starting or ending services. It maintains a database that can be queried using a Windows built-in utility, *sc.exe*. 

This process is the parent to several other key processes: svchost.exe, spoolsv.exe, msmpeng.exe, and dllhost.exe, to name a few.

![services.exe screenshot](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-23%20003633.png)

What is normal?

**Image Path:**  %SystemRoot%\System32\services.exe<br>
**Parent Process:**  wininit.exe<br>
**Number of Instances:**  One<br>
**User Account:**  Local System<br>
**Start Time:**  Within seconds of boot time<br>

What is unusual?

A parent process other than wininit.exe<br>
Image file path other than C:\Windows\System32<br>
Subtle misspellings to hide rogue processes in plain sight<br>
Multiple running instances<br>
Not running as SYSTEM<br><br><br>



## wininit.exe > services.exe > svchost.exe

The **Service Host** (Host Process for Windows Services), or **svchost.exe**, is responsible for hosting and managing Windows services. 

![svchost.exe screenshot](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-23%20004907.png)

What in normal?

Image Path: %SystemRoot%\System32\svchost.exe<br>
Parent Process: services.exe<br>
Number of Instances: Many<br>
Start Time: Typically within seconds of boot time. Other instances of svchost.exe can be started after boot.<br>

What is unusual?

A parent process other than services.exe<br>
Image file path other than C:\Windows\System32<br>
Subtle misspellings to hide rogue processes in plain sight<br>
The absence of the -k parameter<br><br><br>



## lsass.exe

Per Wikipedia, "Local Security Authority Subsystem Service (**LSASS**) is a process in Microsoft Windows operating systems that is responsible for enforcing the security policy on the system. It verifies users logging on to a Windows computer or server, handles password changes, and creates access tokens. It also writes to the Windows Security Log."

![lsass.exe screenshot](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-23%20010930.png)

What is normal?

**Image Path:**  %SystemRoot%\System32\lsass.exe<br>
**Parent Process:**  wininit.exe<br>
**Number of Instances:**  One<br>
**User Account:**  Local System<br>
**Start Time:**  Within seconds of boot time<br>

What is unusual?

A parent process other than wininit.exe<br>
Image file path other than C:\Windows\System32<br>
Subtle misspellings to hide rogue processes in plain sight<br>
Multiple running instances<br>
Not running as SYSTEM<br><br><br>



## winlogon.exe

The **Windows Logon**, **winlogon.exe**, is responsible for handling the **Secure Attention Sequence** (SAS). It is the ALT+CTRL+DELETE key combination users press to enter their username & password.

This process is also responsible for loading the user profile. It loads the user's NTUSER.DAT into HKCU, and userinit.exe loads the user's shell.

It is also responsible for locking the screen and running the user's screensaver, among other functions.

![winlogon.exe process screenshot](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-23%20012012.png)

What is normal?

**Image Path:**  %SystemRoot%\System32\winlogon.exe<br>
**Parent Process:**  Created by an instance of smss.exe that exits, so analysis tools usually do not provide the parent process name.<br>
**Number of Instances:**  One or more<br>
**User Account:**  Local System<br>
**Start Time:**  Within seconds of boot time for the first instance (for Session 1). Additional instances occur as new sessions are created, typically through Remote Desktop or Fast User Switching logons.<br>

What is unusual?

An actual parent process. (smss.exe calls this process and self-terminates)<br>
Image file path other than C:\Windows\System32<br>
Subtle misspellings to hide rogue processes in plain sight<br>
Not running as SYSTEM<br>
Shell value in the registry other than explorer.exe<br><br><br>


## explorer.exe

The last process we'll look at is Windows Explorer, explorer.exe. This process gives the user access to their folders and files. It also provides functionality for other features, such as the Start Menu and Taskbar.

There will be many child processes for explorer.exe.

![explorer.exe process screenshot](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-23%20012818.png)

What is normal?

Image Path:  %SystemRoot%\explorer.exe<br>
Parent Process:  Created by userinit.exe and exits<br>
Number of Instances:  One or more per interactively logged-in user<br>
User Account:  Logged-in user(s)<br>
Start Time:  First instance when the first interactive user logon session begins<br>

What is unusual?

An actual parent process. (userinit.exe calls this process and exits)<br>
Image file path other than C:\Windows<br>
Running as an unknown user<br>
Subtle misspellings to hide rogue processes in plain sight<br>
Outbound TCP/IP connections<br>

![](https://github.com/Andreas512514/core-windows-processes/blob/main/Screenshot%202025-10-23%20013608.png)

The above image is the explorer.exe properties view from Process Explorer.<br><br><br>


If you want more detailed information you can go [here](https://tryhackme.com/room/btwindowsinternals)
