## Threads
  - thread is a lighweight process and basic unit of cpu utilization, it consts of :
    - Program counter
    - register set
    - stack space
  - thread inherits many of the attributes from the parent process, and multile threads can execute concurrently with a single process under a model called multi-threading.
  - If the system has multiple cores then the threads can run in parallel if not then they take turns in execution

  ### Process attributes
   - PID: The kernel assigns a unix ID to every process. Most of the system calls and command that manipulate a process use this PID
   - PPID: In Unix a sytem call never creates a new process directly. Instead, a existing process must clone itself and then exchange the program to be executed. The creating process is called the parent process and the created process is called the child process. In the child process, the PPID is the ID of the parent process and PID is the ID that kernel assigns to the child process
   - UID and EUID: UID is the user id of the process creator, usually the parent process. EUID is the effectice user ID which can be used to restrict permissions to files for the current process. EUID is used in case of setuid and sudo
   - GID and EGID: GID is the group of the process creator, usually the owner of the parent process. GUID is similar to EUID where it can be used to upgrade permissions of the current process and usually set using setguid
   - Niceness: The kernel uses a dynamic algorithm to dermine the amount of CPU time to be allocated to a process. This value can be over-ridden using the "nice value" or the "niceness", so called because it tells how nice your program/process will be to the other processes
   - Control terminal: the control terminal determines the default linkage of standard input, output, and error channels

### New process creation
  - process copies itself with a fork system call
  - fork create a excat copy of the process and kernel gives the child process a new PID
  - fork returns 2 different values, From the child's point of view, it returns 0. The parent receives the child's PID
  - After fork, the child will use one of the `exec` system calls to start the execution of the new program.
  - When the process completes its execution, it calls a routine named `_exit` to notify kernel that it is ready to die. it also supplies with a exit code `0 - success, non-0 errror`
  - Before the process can be allowed to die completely, the kernel requires the parent process to acknowledge the death of the child process. The parent process does this by calling `wait`. The parent receives the exit code of the child process and can request for summary of childs resources.
  - If the parent process dies before the child process, the the init will accept the orphaned child process and call `wait`
