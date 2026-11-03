# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls


```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    int pid;
    pid = fork();

    if (pid == 0)
    {
        printf("I am child, my PID is %d\n", getpid());
        printf("My parent PID is: %d\n", getppid());
        sleep(2);
        exit(0);
    }
    else
    {
        printf("I am parent, my PID is %d\n", getpid());
        wait(NULL);
    }

    return 0;
}
```










##OUTPUT

<img width="596" height="150" alt="image" src="https://github.com/user-attachments/assets/f82f35d8-d84e-47e1-9b48-80c9ad3f6620" />







## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family

```

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main()
{
    int status;

    printf("Running ps with execl\n");
    fflush(stdout);

    if (fork() == 0)
    {
        execl("/bin/ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }

    wait(&status);

    if (WIFEXITED(status))
        printf("Child exited with status: %d\n",
               WEXITSTATUS(status));

    printf("Running ps with execlp (without full path)\n");
    fflush(stdout);

    if (fork() == 0)
    {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }

    wait(&status);

    if (WIFEXITED(status))
        printf("Child exited for execlp with status: %d\n",
               WEXITSTATUS(status));

    printf("Done.\n");

    return 0;
}
```
























##OUTPUT



<img width="745" height="370" alt="image" src="https://github.com/user-attachments/assets/e14ba404-0984-4705-b6b6-d9aae656cdd3" />















# RESULT:
The programs are executed successfully.
