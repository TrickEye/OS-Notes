# Lecture1. Shell Introduction.

## getting started.

First command: `date`

type `date` and you'll get: `Tue Feb 22 16:46:03 CST 2022`

And further: `echo`

type `echo` and any other word, you get the exact word. If you want to echo a sentence with whitespace, you shall use `""`, e.g. `echo "Hello world"`, or, use `\`, e.g. `echo Hello\ world`.

## why do shell understand command?

type `echo $PATH`, you get a series of paths, Shell will search all possible executable programmes in these paths if it matches the command you type in.

---
to find out exactly which directory your command matches, you can use `which xxx`, e.g. `which echo`, Shell will give you the **Path** it interprets, for such instance, you'll get: `/usr/bin/echo`.

## navigating the Shell.

`pwd`, or **Present Working Directory** tells you where you are right now. E.g. use `pwd` right after Shell boot up, you'll see
```BASH
trickeye@TrickEye-SurfaceLaptop3:/mnt/c/Users/TrickEye$ pwd
/mnt/c/Users/TrickEye
```
---
`cd`, AKA **change directory** allows you to navigate Shell using absolute or relative paths. by `cd /home` you'll be at `\home`, or, `.` means the current directory, and `..` means the parent directory, which are two important signs to use if you prefer relative path, e.g. `cd ..`. This is simple. 

And pay attention that in Linux, the root folder is basically just a `/`. This is different from Windows, which contains multiple roots like `C:/`, etc.

---

`ls` lists all files and directories in the **pwd**, or, if you prefer, you can append a path after `ls`, `ls` will list files/directoris in *that* path.

Actually `ls` and many other commands support much more functions. To find out, use `ls --help` which will give you a long list of parameters and their functions. `man ls` provides a different user inferface, or **manual**, with basically the same content as `ls --help`. Press `q` will quit. A useful function of `ls` is `ls -l`, or, `use a long listing format`. To illustrate this, please see: 
```
trickeye@TrickEye-SurfaceLaptop3:/$ ls
bin  boot  dev  etc  home  init  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  snap  srv  sys  tmp  usr  var
```
while
```
trickeye@TrickEye-SurfaceLaptop3:/$ ls -l
total 620
lrwxrwxrwx  1 root root      7 Aug 20  2021 bin -> usr/bin
drwxr-xr-x  1 root root   4096 Aug 20  2021 boot
drwxr-xr-x  1 root root   4096 Feb 22 13:19 dev
drwxr-xr-x  1 root root   4096 Feb 22 13:16 etc
drwxr-xr-x  1 root root   4096 Feb 21 18:23 home
-rwxr-xr-x  1 root root 632096 Feb  9 16:55 init
lrwxrwxrwx  1 root root      7 Aug 20  2021 lib -> usr/lib
lrwxrwxrwx  1 root root      9 Aug 20  2021 lib32 -> usr/lib32
lrwxrwxrwx  1 root root      9 Aug 20  2021 lib64 -> usr/lib64
lrwxrwxrwx  1 root root     10 Aug 20  2021 libx32 -> usr/libx32
drwxr-xr-x  1 root root   4096 Aug 20  2021 media
drwxr-xr-x  1 root root   4096 Feb 21 18:22 mnt
drwxr-xr-x  1 root root   4096 Aug 20  2021 opt
dr-xr-xr-x  9 root root      0 Feb 22 13:16 proc
drwx------  1 root root   4096 Aug 20  2021 root
drwxr-xr-x  1 root root   4096 Feb 22 13:16 run
lrwxrwxrwx  1 root root      8 Aug 20  2021 sbin -> usr/sbin
drwxr-xr-x  1 root root   4096 Aug 20  2021 snap
drwxr-xr-x  1 root root   4096 Aug 20  2021 srv
dr-xr-xr-x 12 root root      0 Feb 22 13:16 sys
drwxrwxrwt  1 root root   4096 Feb 22 13:19 tmp
drwxr-xr-x  1 root root   4096 Aug 20  2021 usr
drwxr-xr-x  1 root root   4096 Aug 20  2021 var
```
Here, the first column tells the accessibility and type. The first character, `d` means it's a directory. And `rwx` means "read, write and execute". if replaced with '-', it means the related group do not have such priviledge.

The first 3 indicates the permissions of the owner of the file, second is for the group which owns the file, third is for everyone.

r, w, x differs between files and directories.

|      |   read   |   write   |  execute  |
| ---- | ---- | ---- | ---- |
|   file   |   see the content of the file   |   add more to it, or delete some of it   |   execute the file   |
|    directory  |   see what's inside, or `cd` into it | rename, create, remove files to the direcotry  |  search    |

---
`cd ~` is another useful tool to change the directory to your home directory. A home directory is usually `/home/YOURUSERNAME`
```
trickeye@TrickEye-SurfaceLaptop3:/$ cd ~
trickeye@TrickEye-SurfaceLaptop3:~$ pwd
/home/trickeye
```

Actually, in Linux file system there are not only files. If you direct to `\sys\class` you will see many name of the devices, e.g. brightness. These are kernal parameters of your system. You'll need root's priviledge to edit it.

## the simplest application

`mv` or move, moves a file. You also use `mv` when you want to rename something. E.g. `mv fileA.txt fileB.txt` renames fileA, or `mv fileA.txt ../fileA.txt` moves fileA.

---
`cp` copies a file, basically the same syntax as `mv`

---
`rm` removes a file, but not a directory. To remove a directory, use `rm -r` to initiate a recursive removal or `rmdir`, for an empty one.

---
`mkdir` establish a new directory. If you want to make a new directory named "hello world", use `mkdir "hello world"`, otherwise you'll make two new directories instead.

---
`cat` shows the content of the file.

---
`Ctrl + l` clears the screen. This shouldn't be a command, but I record it here anyway.

---

`<` redirect input stream, while `>` redirect output stream. This is very handy.
```BASH
echo hello > hello.txt 
cat < hello.txt               # stdout: hello
cat < hello.txt > hello2.txt  # copy a file without `cp`
cat < hello.txt >> hello2.txt # `>>` means append, instead of overwrite.
```

`|` pipe takes the output of the left as the input of the right.
```BASH
ls -l / | tail -n1            # prints the last n(here 1) lines of the `ls -l /` command.
```
a silly example:
```BASH
curl --head --silent google.com | grep -i content-length | cut --delimiter=' ' -f2
```

## the root user
`sudo`, or, do as su(per user), allows you to do something as root user.

maybe you want to modify /sys/class/brightness, and you use
```BASH
echo 500 > brightness       # Not gonna work
sudo echo 500 > brightness  # Not gonna work either
```
this is because the programs on the left and right of the pipe do not know each other. There are many ways to fix it.

`#` means you run the command as root.

`sudo su` sets the status of Shell to root (running as root).

`exit` returns to "running as user".

`tee` command takes input and write to file, also stdout. You can take the advantage by `echo 500 | sudo tee brightness`

---
`xdg-open` opens a file in appropriate program.

## Homework.
课后练习
习题解答 本课程中的每节课都包含一系列练习题。有些题目是有明确目的的，另外一些则是开放题，例如“尝试使用 X 和 Y”，我们强烈建议您一定要动手实践，用于尝试这些内容。 此外，我们没有为这些练习题提供答案。如果有任何困难，您可以发送邮件给我们并描述你已经做出的尝试，我们会设法帮您解答。

本课程需要使用类Unix shell，例如 Bash 或 ZSH。如果您在 Linux 或者 MacOS 上面完成本课程的练习，则不需要做任何特殊的操作。如果您使用的是 Windows，则您不应该使用 cmd 或是 Powershell；您可以使用Windows Subsystem for Linux或者是 Linux 虚拟机。使用echo $SHELL命令可以查看您的 shell 是否满足要求。如果打印结果为/bin/bash或/usr/bin/zsh则是可以的。
```BASH
trickeye@TrickEye-SurfaceLaptop3:/mnt/c/Users/TrickEye$ echo $SHELL
/bin/bash
```
在 /tmp 下新建一个名为 missing 的文件夹。
```BASH
trickeye@TrickEye-SurfaceLaptop3:/mnt/c/Users/TrickEye$ cd /tmp
trickeye@TrickEye-SurfaceLaptop3:/tmp$ mkdir missing
trickeye@TrickEye-SurfaceLaptop3:/tmp$ ls
missing  vscode-git-ca31450e93.sock  vscode-ipc-ec569db0-c6af-4466-b199-4a3fa5948f04.sock
trickeye@TrickEye-SurfaceLaptop3:/tmp$
```
用 man 查看程序 touch 的使用手册。
```BASH
man touch
```
用 touch 在 missing 文件夹中新建一个叫 semester 的文件。
```
trickeye@TrickEye-SurfaceLaptop3:/tmp/missing$ touch semester
```
将以下内容一行一行地写入 semester 文件：
```
 #!/bin/sh
 curl --head --silent https://missing.csail.mit.edu
```
第一行可能有点棘手， # 在Bash中表示注释，而 ! 即使被双引号（"）包裹也具有特殊的含义。 单引号（'）则不一样，此处利用这一点解决输入问题。更多信息请参考 Bash quoting 手册
```BASH
trickeye@TrickEye-SurfaceLaptop3:/tmp/missing$ echo "# !" > semester
trickeye@TrickEye-SurfaceLaptop3:/tmp/missing$ echo "curl --head --silent
 https://missing.csail.mit.edu" >> semester
trickeye@TrickEye-SurfaceLaptop3:/tmp/missing$ cat semester
# !
curl --head --silent https://missing.csail.mit.edu
```

尝试执行这个文件。例如，将该脚本的路径（./semester）输入到您的shell中并回车。如果程序无法执行，请使用 ls 命令来获取信息并理解其不能执行的原因。
```
trickeye@TrickEye-SurfaceLaptop3:/tmp/missing$ ./semester
-bash: ./semester: Permission denied
```
查看 chmod 的手册(例如，使用 man chmod 命令)

使用 chmod 命令改变权限，使 ./semester 能够成功执行，不要使用 sh semester 来执行该程序。您的 shell 是如何知晓这个文件需要使用 sh 来解析呢？更多信息请参考：[shebang](https://zh.wikipedia.org/wiki/Shebang)
```BASH
trickeye@TrickEye-SurfaceLaptop3:/tmp/missing$ chmod u+rwx semester
trickeye@TrickEye-SurfaceLaptop3:/tmp/missing$ ls -l
total 0
-rwxr--r-- 1 trickeye trickeye 55 Feb 22 20:32 semester
trickeye@TrickEye-SurfaceLaptop3:/tmp/missing$ ./semester
HTTP/2 200
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Tue, 11 Jan 2022 16:37:26 GMT
access-control-allow-origin: *
etag: "61ddb246-1f37"
expires: Tue, 22 Feb 2022 12:53:30 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: 6A7A:440D:170208:1BDEC8:6214DA72
accept-ranges: bytes
date: Tue, 22 Feb 2022 12:43:30 GMT
via: 1.1 varnish
age: 0
x-served-by: cache-hkg17931-HKG
x-cache: MISS
x-cache-hits: 0
x-timer: S1645533811.726675,VS0,VE263
vary: Accept-Encoding
x-fastly-request-id: 39f330bd62b1813b0f57ef742014a91aee37901c
content-length: 7991
```
使用 | 和 > ，将 semester 文件输出的最后更改日期信息，写入主目录下的 last-modified.txt 的文件中

写一段命令来从 /sys 中获取笔记本的电量信息，或者台式机 CPU 的温度。注意：macOS 并没有 sysfs，所以 Mac 用户可以跳过这一题。