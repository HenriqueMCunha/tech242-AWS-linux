# Processes

Processes are usually run in the background and are run by the operating system.
They are in memory and look like they're possibly using the CPU:
* Sometimes they give the appearance that they're being processed but they may in fact be just present in memory.
* If a Virtual machine only has one core, it can only process one process at a time and will be constantly switching between processes.
* The VM will be giving a bit of CPU time to each process whilst another running process has to wait in queue to get its instructions done.

## Two types of Processes

### User Processes 

A user process is a running instance of a program that is started and controlled by a user.
These processes are typically initiated by the user's actions, such as running a command in a terminal.

We can use the command `ps` to check which user processes are running:

![Screenshot-user-processes-ps.png](../readme-images/Screenshot-user-processes-ps.png)

By using the `ps` command you will get the following information:
* PID - process ID, number that identifies each individual process.
* TTY - TeleTYpewriter, which indicates the terminal from which the process was started.
* TIME - 
* CMD - 

It is possible for more than one user to login via SSH to the same virtual machine at the same time.
Each terminal session also has an id and will have different processes specific to that terminal session.

### System Processes

System processes are initiated by the operating system itself to perform essential tasks such as managing hardware, scheduling tasks, and handling system events.
System processes don't provide an application or interface for the end user to actually use.
* They provide, drivers, login, file, print services. 
* It is like a middleman between hardware and software.