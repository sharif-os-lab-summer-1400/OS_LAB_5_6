---
name: فرم گزارش آزمایش پنجم
about: برای نوشتن گزارش آزمایشگاه از این تمپلیت استفاده کنید
title: Session 5 Report
labels: documentation
assignees: mhaghighat20

---

Team Name: `[FILL HERE]`

Student Name of member 1: `[FILL HERE]`
Student No. of member 1: `[FILL HERE]`

Student Name of member 2: `[FILL HERE]`
Student No. of member 2: `[FILL HERE]`

- [x] Read Session Contents.

### Section 5.3.1

- [x] Write the `Hello World!` program
    - [x] `FILL HERE with your source code`
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <unistd.h>
    #include <string.h>
    #include <sys/wait.h>
    int main() {
        char * msg="Hello World!";
        int msg_len = strlen(msg)+1;
        int fd[2];
        if (pipe(fd) < 0) {
            printf("couldn't pipe\n");
            return 1;
        }
        int pid = fork();
        if (pid < 0) {
            printf("couldn't fork\n");
            return 1;
        } else if (pid == 0) {
            close(fd[1]);
            char buf[msg_len];
            read(fd[0], buf, msg_len);
            printf("%s\n", buf);
            exit(0);
        } else {
            close(fd[0]);
            write(fd[1], msg, msg_len);
            wait(NULL);
        }
        return 0;
    }
    ```
    
- [x] Write the `ls` to `wc` program
    - [x] `FILL HERE with your source code`
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <unistd.h>
    #include <sys/wait.h>
    int main() {
        int fd[2];
        if (pipe(fd) < 0) {
            printf("couldn't pipe\n");
            return 1;
        }
        int pid = fork();
        if (pid < 0) {
            printf("couldn't fork\n");
            return 1;
        }
        if (pid == 0) {
            close(fd[1]);
            dup2(fd[0], 0);
            execl("/usr/bin/wc", "wc", (char*) NULL);
        } else {
            close(fd[0]);
            dup2(fd[1], 1);
            execl("/bin/ls", "ls");
        }
        return 0;
    }
    ```

- [x] Investigate how to have a bi-direction pipe
    - [x] `FILL HERE with your descriptions`
    
    <div dir="ltr">
     می توان از دو عدد 
    pipe
    میان پدر و فرزند بدین صورت استفاده کرد که اولین
    pipe
    برای خواندن فرزند و نوشتن پدر استفاده می شود و دومین 
    pipe
    برای خواندن پدر و نوشتن فرزند استفاده می شود.
    
    همچنین میتوان به جای 
    pipe
    از
    named pipe
    یا
    FIFO
    استفاده کرد.
    طول عمر این گونه
    pipe
    ها مستقل از طول عمر پردازه ها میباشد و همانند یک فایل بوده و با دستور 
    mkfifo
    میتوان آنها را تولید کرد.
    بنابراین پردازه ها با خواندن و نوشتن در یک فایل، با یک دیگر ازتباط دو طرفه داشته باشند.
    همچنین با استفاده از این نوع
    pipe
    ها میتوان دو پردازه که در دو سیستم عامل جداگانه هستند تحت شبکه به هم متصل کرد.
    </div>
    

### Section 5.3.2

- [ ] Describe the usecase of different signals:
    1. [ ] `[FILL HERE with the description for SIGINT.]`
    1. [ ] `[FILL HERE with the description for SIGHUP.]`
    1. [ ] `[FILL HERE with the description for SIGSTP.]`
    1. [ ] `[FILL HERE with the description for SIGCONT.]`
    1. [ ] `[FILL HERE with the description for SIGKILL.]`

- [ ] Describe SIGALRM
    1. [ ] `[FILL HERE with your description.]`

- [ ] Investigate the given code
    1. [ ] `[FILL HERE with your description.]`
    1. [ ] `[FILL HERE with screenshot of program execution]`

- [ ] Modify the given program by handling SIGALRM
    1. [ ] `[FILL HERE with your source code.]`

- [ ] Write a program that handles Ctrl + C
    1. [ ] `[FILL HERE with your source code.]`
