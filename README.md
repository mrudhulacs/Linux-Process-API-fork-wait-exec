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

```
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

```


## OUTPUT

<img width="606" height="257" alt="Screenshot 2025-09-22 203903" src="https://github.com/user-attachments/assets/5834580e-8f10-4502-9089-ce7a62ea6e66" />








## 2 . C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family


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


<img width="697" height="554" alt="Screenshot 2025-09-22 204212" src="https://github.com/user-attachments/assets/bb704c8f-fdcd-4b99-9b8e-c01805ad6ec2" />


<img width="756" height="604" alt="Screenshot 2025-09-22 204224" src="https://github.com/user-attachments/assets/48488465-605c-4deb-981b-074dd07d97a7" />


<img width="694" height="600" alt="Screenshot 2025-09-22 204233" src="https://github.com/user-attachments/assets/6b014b89-2307-4c79-a824-6923160f867d" />


<img width="710" height="527" alt="Screenshot 2025-09-22 204245" src="https://github.com/user-attachments/assets/02a00579-7023-4d23-853c-e97ba153672c" />


<img width="741" height="530" alt="Screenshot 2025-09-22 204255" src="https://github.com/user-attachments/assets/68859fa4-0653-47ae-9a33-ce8c2572b515" />


<img width="753" height="524" alt="Screenshot 2025-09-22 204306" src="https://github.com/user-attachments/assets/91c53f6d-ae40-40fe-a645-5bbd665757dc" />


<img width="731" height="557" alt="Screenshot 2025-09-22 204322" src="https://github.com/user-attachments/assets/f2ef82b8-1087-43af-bdaf-0dca2708848b" />


<img width="708" height="405" alt="Screenshot 2025-09-22 204333" src="https://github.com/user-attachments/assets/1250f21a-5b37-4cf6-b565-4d9ba4ce3eba" />


## 3. C Program to execute Linux system commands using Linux API system calls exec() family

```
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
```

## OUTPUT 


<img width="752" height="366" alt="Screenshot 2025-09-22 204547" src="https://github.com/user-attachments/assets/2bb65620-344d-418c-9216-42cc4ed6aedc" />




## RESULT:
The programs are executed successfully.
