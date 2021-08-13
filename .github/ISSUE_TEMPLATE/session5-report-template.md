---
name: فرم گزارش آزمایش پنجم
about: برای نوشتن گزارش آزمایشگاه از این تمپلیت استفاده کنید
title: Session 5 Report
labels: documentation
assignees: mhaghighat20

---

Team Name: 97110285-97101286

Student Name of member 1: Mohammadreza Abdi
Student No. of member 1: 97110285

Student Name of member 2: Alireza Ilami
Student No. of member 2: 97101286

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
    
    <div dir="rtl">
     
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
    بنابراین پردازه ها با خواندن و نوشتن در یک فایل، با یک دیگر ارتباط دو طرفه داشته باشند.
    همچنین با استفاده از این نوع
    pipe
    ها میتوان دو پردازه که در دو سیستم عامل جداگانه هستند تحت شبکه به هم متصل کرد.
    </div>
    

### Section 5.3.2

- [x] Describe the usecase of different signals:
    1. [x] `[FILL HERE with the description for SIGINT.]`
    2. [x] `[FILL HERE with the description for SIGHUP.]`
    3. [x] `[FILL HERE with the description for SIGSTP.]`
    4. [x] `[FILL HERE with the description for SIGCONT.]`
    5. [x] `[FILL HERE with the description for SIGKILL.]`

    <div dir="rtl">
    
    1. SIGINT:
    هنگام وقفه توسط کیبورد تولید می شود و به پردازه پرتاب می شود.
    (ctrl + c)
    
    2. SIGHUP:
    هنگام بسته شدن ترمینال کنترل کننده یک پردازه تولید می شود و به آن پردازه پرتاب می شود.
    
    3. SIGSTOP:
    هنگامی که یک پردازه در حال اجرا متوقف می شود تولید می شود.
    
    4. SIGCONT:
    هنگام ادامه دادن یک پردازه متوقف شده ایجاد شده و پرتاب می شود.
    
    5. SIGKILL:
    هنگام نابود شدن یک پردازه تولید شده و پرتاب می شود. 
    </div>

- [x] Describe SIGALRM
    1. [x] `[FILL HERE with your description.]`
 
    <div dir="rtl">
    
    تابع
    alarm
    منجر به پرتاب شدن سیگنال 
    SIGALRM
    بعد از گذشت تعداد ثانیه هایی است که در ورودی این تابع داده شده است.
    به صورت پیش فرض پردازه هنگام مواجه با سیگنال
    SIGALRM
    خاتمه میابد اما میتوان آن را مدیریت کرد.
    هر پردازه تنها می تواند یکبار از این تابع استفاده کند و چندین بار استفاده از تابع 
    alarm
    منجر به
    reset
    شدن زمانبند ساعت پردازه خواهد شد.
    (به اصطلاح 
    alram
    ها پشته نخواهند شد.)
    </div>

- [x] Investigate the given code
    1. [x] `[FILL HERE with your description.]`
    
    <div dir="rtl">
    
    برنامه با توجه به خط
    while(1)
    در یک حلقه بینهایت میافتد، اما چون قبل از آن دستور
    alarm(5)
    جرا شده، بعد از گذشت 5 ثانیه برنامه متوقف شده و خاتمه میابد. بنابراین اولین
    printf
    که قبل از 
    while
    بوده اجرا می شود ولی دومین 
    printf
    که بعد از
    while
    میباشد، اجرا نخواهد شد و پردازه مستقیما توسط سیگنال
    SIGALRM
    متوقف خواهد شد.
    </div>
    
    3. [x] `[FILL HERE with screenshot of program execution]`

    ![image](https://user-images.githubusercontent.com/45341111/129383390-665ba6a9-ecbf-4995-b47e-9d6f1d52c02f.png)


- [x] Modify the given program by handling SIGALRM
    1. [x] `[FILL HERE with your source code.]`

    ```c
    #include <stdio.h>
    #include <unistd.h>
    #include <signal.h>

    void handler(){
        return;
    }

    int main() {
        signal(SIGALRM, handler);
        alarm (5);
        printf ("Looping forever . . . \n");
        pause();
        printf("This line should never be executed\n");
        return 0;
    }
    ```

- [x] Write a program that handles Ctrl + C
    1. [x] `[FILL HERE with your source code.]`

    ```c
    #include <stdio.h>
    #include <unistd.h>
    #include <signal.h>

    void handler(){
        return;
    }

    int main() {
        signal(SIGINT, handler);
        printf ("interrupt to continue . . . \n");
        pause();
        printf ("waiting for second time interruption . . . \n");
        pause();
        printf("program ended.\n");
        return 0;
    }
    ```
