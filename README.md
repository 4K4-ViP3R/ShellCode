# ShellCode

## What is ShellCode?

There is no any similarity between shellcode and shell scripting. Then why shellcode? Shellcode is an instance of 
a command line interpreter that use to exploit existing vulnerabilities in the target system or a program to get remote shell. 
Attackers could use that remote shell to access and more interaction with the victim's system (Target System). 
It is very simple. Using several lines of code, we can gain the new remote shell from the victim's machine. 
Spawning new remote shell is a very lightweight process and very efficient.

```javascript
#include <stdio.h>
#include <unistd.h>
int main()
{
	char *args[2];
	args[0] = "/bin/sh";
	args[1] = NULL;
	execve("/bin/sh", args, NULL);
	return 0;
}
```
The above standard C code will spawn a shell. Using a proper editor, you can compile and run it very easily. The main point 
of this remote shell gaining process using shellcode is that if the target program is running in the system with 
some level of privileges, the newly popped the remote shell has the same privileges. 
It can be low level or high-level privileges.

The below code is compiled version of the above shellcode

```javascript
.LC0:
        .string "/bin/sh"
main:
        push    rbp
        mov     rbp, rsp
        sub     rsp, 16
        mov     QWORD PTR [rbp-16], OFFSET FLAT:.LC0
        mov     QWORD PTR [rbp-8], 0
        lea     rax, [rbp-16]
        mov     edx, 0
        mov     rsi, rax
        mov     edi, OFFSET FLAT:.LC0
        call    execve
        mov     eax, 0
        leave
        ret
```
Below I briefly explain how to convert C language source code into executable. Try it using your terminal.

### STEP 01 - Pre-processing

Pre-processing is mandatory if you use C or C++ source code. because it helps to handle all '#' directives.<br/>
Command:
- cc -E -o yourScriptName.pp.c yourScriptName.c
<img src="images/SS2.png">
![](images/SS%202.png)

### STEP 02 - Compilation

This helps to convert high level language into the specific set of instructions.<br/>
Command:
- gcc -S yourScriptName.c

### STEP 03 - Assembler

This helps to convert assembly to binary.<br/>
Command:
- gcc -c yourScriptName.c --> (Produce yourScriptName.o file)

### STEP 04 - Create executable file

Command:
- gcc -o yourFileName yourScriptName.o
