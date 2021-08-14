---
name: فرم گزارش آزمایش ششم
about: برای نوشتن گزارش آزمایشگاه از این تمپلیت استفاده کنید
title: Session 6 Report
labels: documentation
assignees: mhaghighat20

---

Team Name: 97110285-97101286

Student Name of member 1: Mohammadreza Abdi
Student No. of member 1: 97110285

Student Name of member 2: Alireza Ilami
Student No. of member 2: 97101286

- [x] Read Session Contents.

## Section 6.4

- [x] Using `malloc` and `free` in program
    - [x] ![image](https://user-images.githubusercontent.com/45389577/128612418-359c9b0d-a2af-429c-b8a0-84a91e32e29b.png)
    - [x] ![image](https://user-images.githubusercontent.com/45389577/128612407-50362ed1-b715-4e7a-801b-2b76775d598f.png)

    
- [x]  Using `ps`
    - [x] ![image](https://user-images.githubusercontent.com/45389577/128612454-bf484bf1-d1ec-454a-8d4e-5490e2ef8c9e.png)
    - [x] Columns:
        User: Shows the user who runs this process.
        VSZ: Virtual System Size. (Memory) including swap, and shared memories. This process has access to this memory size.
        RSS: Resident Set Size. the amount of memory reserved for this process in the RAM. not including swap but contains shared memory as long as it is in RAM.
        %MEM: RSS to Physical memory ratio.
        COMMAND: the name of the process
           
- [x]  Getting started with memory segments
    - [x] ![image](https://user-images.githubusercontent.com/45389577/128613170-83d6844f-3bc3-4c82-99d0-2af8e561886b.png)
    - [x] ![image](https://user-images.githubusercontent.com/45389577/128613184-bc2246c0-c655-46cc-9753-b0a3895623f2.png)
    - [x] Heap and Stack are not shown. Because they are not constant. They are dynamic and related to the runtime.
    

- [x] Getting started with memory sharing
    1. [x] ![image](https://user-images.githubusercontent.com/45389577/128613248-aca12b4f-8b02-4734-8d55-03c589137751.png)
    1. [x] ![image](https://user-images.githubusercontent.com/45389577/128613266-52c4ee67-c08c-420b-94a9-633ff6757cde.png)
    1. [x] cat, mkdir, and rm:
           ![image](https://user-images.githubusercontent.com/45389577/128613304-996db023-d47c-4ef3-b22d-2fd4155b296c.png)


- [ ] Getting started with addresses
    1. [x] The address of etext symbol indicates the end of a program segment. In other words, This is the first address past the emd of the text segment (the program code). It is not defined in any header file. the program must declare it. Although this symbol has been provided on most UNIX systems, they are not standardized and should be used carefully.
    2. [ ] `[FILL HERE with your screenshots of given program analysis]`
    3. [ ] `[FILL HERE with your screenshots of sbrk analysis]`
    4. [ ] `[FILL HERE with your screenshots & code of heap growth analysis]`

