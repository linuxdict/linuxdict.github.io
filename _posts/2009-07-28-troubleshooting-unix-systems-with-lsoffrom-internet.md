---
id: 438
title: Troubleshooting UNIX Systems with Lsof(From Internet)
date: 2009-07-28T01:51:49+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=438
permalink: /2009-07-troubleshooting-unix-systems-with-lsoffrom-internet/
bttc_cache:
  - 1273344709:0
  - 1273344709:0
categories:
  - Howto
tags:
  - linux
  - tips
---
So excellent articles, but the blogspot.com is blocked by STH. so i paste it here.
  
Original Link: http://0xfe.blogspot.com/2006/03/troubleshooting-unix-systems-with-lsof.html

One of the least-talked-about tools in a UNIX sysadmin&#8217;s toolkit is lsof. Lsof lists information about files opened by processes. But that&#8217;s really an understatement.

Most people forget that, in UNIX, (almost) everything is a file. The OS makes hardware available to applications by way of files in /dev. Kernel, system, memory, device etc. information in made available inside files in /proc. TCP/UDP sockets are sometimes represented internally as files. Even directories are really just files containing other filenames.
  
<!--more-->


  
Lsof works by examining kernel data-structures and provides a variety of information related to files, pipes, sockets and more.

Lsof is installed by default on most Linux distributions, BSD distributions and OS X. Binary packages for Solaris, AIX, HP-UX, \*cough\*SCO OpenServer\*cough\* and many other UNIXes (Unices?) are available on the web.

So, just how useful is lsof?

Deciphering its Output

Switch to root, and type lsof on the commandline.

linux# lsof
  
COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME
  
init 1 root cwd DIR 3,65 4096 2 /
  
init 1 root rtd DIR 3,65 4096 2 /
  
init 1 root txt REG 3,65 29556 172317 /sbin/init
  
init 1 root mem REG 3,65 1166880 93908 /lib/libc-2.3.5.so
  
init 1 root mem REG 3,65 103053 93909 /lib/ld-2.3.5.so
  
init 1 root 10u FIFO 3,65 48438 /dev/initctl
  
ksoftirqd 2 root cwd DIR 3,65 4096 2 /
  
ksoftirqd 2 root rtd DIR 3,65 4096 2 /
  
ksoftirqd 2 root txt unknown /proc/2/exe
  
events/0 3 root cwd DIR 3,65 4096 2 /
  
events/0 3 root rtd DIR 3,65 4096 2 /
  
events/0 3 root txt unknown /proc/3/exe

&#8230;SNIP&#8230;

syslog-ng 6529 root txt REG 3,69 114132 84690 /usr/sbin/syslog-ng
  
syslog-ng 6529 root mem REG 3,65 1166880 93908 /lib/libc-2.3.5.so
  
syslog-ng 6529 root mem REG 3,65 64568 93943 /lib/libresolv-2.3.5.so
  
syslog-ng 6529 root mem REG 3,65 75176 93924 /lib/libnsl-2.3.5.so
  
syslog-ng 6529 root mem REG 3,65 103053 93909 /lib/ld-2.3.5.so
  
syslog-ng 6529 root 0u CHR 1,3 47320 /dev/null
  
syslog-ng 6529 root 1u CHR 1,3 47320 /dev/null
  
syslog-ng 6529 root 2u CHR 1,3 47320 /dev/null
  
syslog-ng 6529 root 3u unix 0xdea00e00 672127 /dev/log

&#8230;SNIP&#8230;

asterisk 7001 root 10u IPv4 6015 TCP localhost:5038 (LISTEN)
  
asterisk 7001 root 11r FIFO 3,70 306 /var/run/asterisk/autod
  
ial.ctl
  
asterisk 7001 root 12u IPv4 6834 UDP *:5060
  
asterisk 7001 root 13r FIFO 0,5 6019 pipe
  
asterisk 7001 root 14u IPv4 6016 TCP localhost:5038->localho
  
st:32768 (ESTABLISHED)
  
asterisk 7001 root 15u IPv4 6835 UDP *:2727
  
asterisk 7001 root 16u IPv4 6861 UDP *:4569
  
asterisk 7001 root 17u REG 3,70 0 593222 /var/lib/asterisk/astdb
  
asterisk 7001 root 18r FIFO 0,5 6883 pipe
  
asterisk 7001 root 19u REG 3,70 39402 32066 /var/tmp/iaxy.bin-19098
  
89093 (deleted)
  
asterisk 7001 root 20w FIFO 0,5 6883 pipe

&#8230;LOTS MORE SNIPPED&#8230;

What you will be presented with is a very long list of open files, which you might want to pipe through your favourite pager.

By default (on Linux), lsof displays the following information about each open file:

* COMMAND: The name of the UNIX command associated with the process.

* PID: The Process ID.

* USER: The user ID or login name of the user to whom the process belongs.

* FD: The file descriptor number of the file or a code representing more information about the structure. See manual page for details.

* TYPE: The type of the node associated with the file. E.g. REG signifies a regular file, IPv4 or IPv6 signifies an IP socket, DIR a directory, &#8220;unix&#8221; a UNIX domain socket, etc.

* DEVICE: Usually contains major and minor device numbers for the files, or addresses/references for other structures.

* SIZE: The size of the file or the file offset, in bytes. (If available.) In the case of files that don&#8217;t have true sizes (eg., sockets, pipes), lsof displays the size of the content their kernel buffer descriptors.

* NODE: Node number / inode / Internet protocol type (TCP) etc.

* NAME: The name of the file / mount point / device / Internet address / etc.

For a comprehensive description of these fields, refer the lsof manual page.

Since lsof works by examining kernel memory, you will need root access to be able to fully utilize it. A non-root user will not have access to information that belongs to other users.

Common Usage

Lsof is usually run with one or more of the following options:

* /path/to/file: List processes, owners and open file descriptors that are currently using the specified file.

* -i \[46\]\[protocol\]\[@hostname|hostaddr\]\[:service|port\]: List Internet files / sockets.

* -u name: List files owned by user.

* -p pid: List files open by specified process.

* -t: Terse output. No headers, only PIDs. Useful within scripts.

* -n: Disable resolving of network names.

* -N: List NFS files

These options are ORed by default.

Display all internet files OR files opened by user &#8220;foobar&#8221;.

\# lsof -u foobar -i

To display all internet files that are opened by foobar, you need to apply the AND (-a) condition between the switches.

\# lsof -u foobar -a -i

The following recipes demonstrate how lsof can be used to troubleshoot real-world problems.

Recipe #1: Finding Port Hogs

Your web-server is refusing to come up because port 80 is in use by another process. How do you track down the offending process?

\# lsof -i

&#8230; SNIP &#8230;

asterisk 7554 root 16u IPv4 6861 UDP *:4569
  
postmaste 7688 postgres 5u IPv4 5955 UDP localhost:32768->localhost:32768
  
postmaste 7689 postgres 5u IPv4 5955 UDP localhost:32768->localhost:32768
  
sshd 27038 root 3u IPv4 677971 TCP reddwarf:ssh->CPE.xxxx.com:61702 (ESTABLISHED)
  
sshd 27043 mohit 3u IPv4 677971 TCP reddwarf:ssh->CPE.xxxx.com:61702 (ESTABLISHED)

&#8230; SNIP &#8230;

Nice. A list of open Internet sockets, along with the processes, addresses and owners. Also note that (similar to netstat), the TCP states are displayed. Above, we can see two established ssh sessions in progress.

Let&#8217;s add a port filter and find exactly what we&#8217;re looking for.

\# lsof -i TCP:80
  
COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME
  
lighttpd 7356 lighttpd 3u IPv4 6409 TCP *:http (LISTEN)

Okay, so lighttpd is the reason why Apache won&#8217;t run. That&#8217;s probably a good thing.

Recipe #2: Finding Processes Within a Given Port Range

You need to find a range of free ports for your new multimedia application.

\# lsof -i TCP:5000-5200
  
COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME
  
asterisk 7001 root 10u IPv4 6015 TCP localhost:5038 (LISTEN)
  
asterisk 7001 root 14u IPv4 6016 TCP localhost:5038->localhost:32768 (ESTABLISHED)
  
asterisk 7002 root 10u IPv4 6015 TCP localhost:5038 (LISTEN)
  
asterisk 7002 root 14u IPv4 6016 TCP localhost:5038->localhost:32768 (ESTABLISHED)
  
asterisk 7039 root 10u IPv4 6015 TCP localhost:5038 (LISTEN)
  
asterisk 7039 root 14u IPv4 6016 TCP localhost:5038->localhost:32768 (ESTABLISHED)
  
asterisk 7040 root 10u IPv4 6015 TCP localhost:5038 (LISTEN)
  
asterisk 7040 root 14u IPv4 6016 TCP localhost:5038->localhost:32768 (ESTABLISHED)
  
asterisk 7041 root 10u IPv4 6015 TCP localhost:5038 (LISTEN)
  
asterisk 7041 root 14u IPv4 6016 TCP localhost:5038->localhost:32768 (ESTABLISHED)
  
asterisk 7042 root 10u IPv4 6015 TCP localhost:5038 (LISTEN)
  
asterisk 7042 root 14u IPv4 6016 TCP localhost:5038->localhost:32768 (ESTABLISHED)
  
asterisk 7044 root 10u IPv4 6015 TCP localhost:5038 (LISTEN)
  
asterisk 7044 root 14u IPv4 6016 TCP localhost:5038->localhost:32768 (ESTABLISHED)
  
perl 7046 root 3u IPv4 6054 TCP *:5100 (LISTEN)
  
perl 7046 root 4u IPv4 6055 TCP *:5101 (LISTEN)
  
perl 7046 root 6u IPv4 6056 TCP localhost:32768->localhost:5038 (ESTABLISHED)
  
asterisk 7073 root 10u IPv4 6015 TCP localhost:5038 (LISTEN)
  
asterisk 7073 root 14u IPv4 6016 TCP localhost:5038->localhost:32768 (ESTABLISHED)
  
asterisk 7504 root 10u IPv4 6015 TCP localhost:5038 (LISTEN)
  
asterisk 7504 root 14u IPv4 6016 TCP localhost:5038->localhost:32768 (ESTABLISHED)

Recipe #3: Listing User Files

What files do users &#8220;foobar&#8221; and &#8220;apache&#8221; have open?

\# lsof -u foobar,apache

List UDP ports in use by user &#8220;mohit&#8221;.

\# lsof -i UDP -a -u mohit

Who&#8217;s responding to &#8220;who&#8221;?

\# lsof -i UDP:who

Recipe #4: Unmounting a Disk or Filesystem

Sometimes you need to track down the user or process that&#8217;s blocking you from unmounting a disk.

\# umount /opt
  
umount: /opt: device is busy
  
umount: /opt: device is busy
  
\# mount | grep &#8220;/opt&#8221;
  
/dev/hdb9 on /opt type ext3 (rw,noatime)
  
\# lsof /dev/hdb9
  
COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME
  
perl 7046 root 2w REG 3,73 111 1376386 /opt/local/paynacea/var/state/callmanager.pid.err
  
perl 7046 root 5w REG 3,73 6783 1376385 /opt/local/paynacea/var/log/callmanager.log
  
\# kill 7046
  
\# umount /opt

Or the simpler:

\# kill \`lsof -t /opt\`

Recipe #5: Finding Device Hogs

Who&#8217;s using the audio manager?

\# lsof /dev/audio

Why can&#8217;t I start my alternate logger?

\# lsof /dev/log

Why doesn&#8217;t my CD eject?

\# lsof /dev/cdrom

Recipe #6: Using Exclusions

The &#8216;^&#8217; (negated) modifier can prefix the User or Process ID parameters to exclude them from the resulting list. Since they represent exclusions, they are applied without ORing or ANDing and take effect before any other selection criteria are applied.

List all Internet files/sockets open by non-root users.

\# lsof -i -u^root

Recipe #7: Recursing Directories

The &#8216;+D&#8217; option causes lsof to search for open files within a specified directory, recursing down to its complete depth.

List all processes that have files open in /tmp.

\# lsof +D /tmp

The &#8216;+d&#8217; option does the same thing, but does \_not\_ descend the directory tree.

Recipe #8: Matching by Process Name

List all files open by processes beginning with the letters mpg.

\# lsof -c mpg

Using a regular-expression.

\# lsof -c &#8216;/post.*er/&#8217;

Recipe #9: Examining Suspicious Processes

Lsof can be used along with strace to examine and monitor the operation of viruses, worms or spyware.

What files are opened by PID 14554?

\# lsof -p 14554

Who&#8217;s looking at the password file?

\# lsof /etc/passwd

Recipe #10: Repeat Mode

The -r switch puts lsof in repeat mode. It delays every 15 seconds (unless specified), and displays another listing.

Watching a user&#8217;s open files every 5 seconds:

\# lsof -u badcop -r5 

Monitoring the password file:

\# lsof /etc/passwd -r 2

Recipe #11: Finding Deleted Open Files

This recipe was added on 26/Mar/06 after an anonymous poster left a comment regarding deleted files.

One of the most annoying problems is a file-system quickly running out of space, without a hint of what file is responsible for it. This happens when a file (usually a log-file), gets deleted while it&#8217;s still being written to. When you delete an open file, the kernel unlinks the file from the directory, but cannot remove the inode, since it&#8217;s still open.

This causes the file to continue to grow, with no trace of its existance anywhere. Well&#8230; almost anywhere.

Lsof provides the +L parameter to list the number of link counts an open file has. When followed by a number, lsof only displays files with link counts less thatn the specified number.

mohit@reddwarf ~ $ lsof +L3
  
COMMAND PID USER FD TYPE DEVICE SIZE NLINK NODE NAME
  
sshd 11540 mohit mem REG 3,69 303448 1 85869 /usr/sbin/sshd
  
sshd 11540 mohit mem REG 3,65 35404 1 94075 /lib/libnss_nis-2.3.5.so
  
sshd 11540 mohit mem REG 3,65 30928 1 94086 /lib/libnss_compat-2.3.5.so
  
sshd 11540 mohit mem REG 3,65 35236 1 93958 /lib/libnss_files-2.3.5.so
  
sshd 11540 mohit mem REG 3,65 28444 1 94094 /lib/libcrack.so.2.8.0

A deleted file has zero links. So the following command displays deleted-but-open files on a system.

$ lsof +L1

Display a list of deleted-but-open files within a specific filesystem.

$ lsof +aL1 /tmp

Finally

We barely scratched the surface with the above recipes, but as you can see, lsof is a powerful troubleshooting tool. I&#8217;d be interested in learning what other users do with lsof. Toy with it, tinker with it, use it and let me know how it has helped you.