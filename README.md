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

## 1. C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pid = fork();

    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(2);  // Keep child alive for verification
    } else { 
        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL); 
    }
}




## OUTPUT
<img width="642" height="333" alt="image" src="https://github.com/user-attachments/assets/61f9513c-8ac9-4293-b44b-88d5db634803" />


## 2. C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family
```
#include <stdlib.h>
#include <sys/wait.h>
#include <sys/types.h>
int main()
{       int status;
        printf("Running ps with execlp\n");
        execl("ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                puts("child did not exit successfully\n");
        printf("Done.\n");
printf("Running ps with execlp. Now with path specified\n");
        execl("/bin/ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                puts("child did not exit successfully\n");
        printf("Done.\n");
        exit(0);}
  
```

## OUTPUT

<img width="745" height="599" alt="b" src="https://github.com/user-attachments/assets/af30b983-a6c0-4ef6-940c-ed3c45a07718" />
<img width="668" height="589" alt="c" src="https://github.com/user-attachments/assets/a893d178-a7a9-430e-aa83-d10068fcd71d" />
<img width="723" height="590" alt="d" src="https://github.com/user-attachments/assets/728764f2-0f7b-48e4-9223-77afa4515976" />
<img width="710" height="593" alt="e" src="https://github.com/user-attachments/assets/331723ca-3530-47b0-8256-d9c33a2e9fa3" />
<img width="786" height="589" alt="f" src="https://github.com/user-attachments/assets/965da45b-f54d-40d5-93bf-8880d00a8074" />
<img width="792" height="585" alt="g" src="https://github.com/user-attachments/assets/3b7582e4-64f2-434d-b60d-f77affeda67d" />
<img width="771" height="600" alt="h" src="https://github.com/user-attachments/assets/ded2e5eb-4cf5-42cd-9989-a4f1b5713173" />
<img width="749" height="603" alt="j" src="https://github.com/user-attachments/assets/a0820306-745a-43da-96c1-e3fdaaf65ce1" />
<img width="728" height="199" alt="k" src="https://github.com/user-attachments/assets/7038e8dd-0b7d-4633-a1b0-2a7ca5676d38" />




## 3. C Program to execute Linux system commands using Linux API system calls exec() family

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    
    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Done.\n");
    return 0;
}

## OUTPUT

<img width="682" height="422" alt="Screenshot 2025-09-24 103750" src="https://github.com/user-attachments/assets/9785f406-e5b1-4ad7-9049-a2c7a72f3177" />


# RESULT:
The programs are executed successfully.
