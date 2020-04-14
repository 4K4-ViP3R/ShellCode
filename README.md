# ShellCode

What is ShellCode?

There are no any similarity between shellcode and shell scripting. Then why shellcode? Shellcode is an instance of a command line interpreter that use to exploit existing vulnerabilities in the target system or a program to get remote shell. Attackers could use that remote shell to access and more interaction with the victim's system (Target System). It is very simple. Using several lines of code we can gain the new remote shell from the victim's machine. Spawning new remote shell is a very lightweight process and very efficient.

#include <stdio.h>
int main()
{
	char *args[2];
	args[0] = "/bin/sh";
	args[1] = NULL;
	execve("/bin/sh", args, NULL);
	return 0;
}

The above standard C code will spawn a shell. Using a proper editor you can compile and run it very easily. The main point of this remote shell gaining process using shellcode is that if the target program is running in the system with some level of privileges, the newly popped the remote shell has the same privileges. It can be low level or high level privileges.

