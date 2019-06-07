---
layout: post
title:  "Over The Wire - Wargames"
date:   2018-07-03 12:18:31 -0700
categories: wargames 
---

[OverTheWire](http://overthewire.org/wargames/) is a series of wargames designed to help you practice security concepts. I started out with wargames on the first machine, Bandit, just to gauge the level of difficulty of the wargames offered by OTW. Compared to the more well-known capture-the-flag contests, like Google's CTF or the DefCon CTFs, OTW offers more rudimentary puzzles / hacks, but it's still an excellent resource for refreshing one's security-related skillsets.

**NOTE - May 2019** Over the coming weeks we'll be transfering each exercise to its own page and will add comprehensive write-ups for each level in which we explain the commands used in detail (required parameters, optional parameters, the OSX analogous commands to the Linux commands used, etc.)

## level_0
This level's a freebie. Simply `ssh` into the bandit machine and you're done with level 0:

`ssh bandit0@bandit.labs.overthewire.org -p 2220`

## level_0 -> 1

The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

```console
bandit0@bandit:~$ ls
readme

bandit0@bandit:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

We terminate our session so that we can log into bandit1:
`bandit0@bandit:~$ exit`

## level_1 -> 2
As before, we `ssh` into the `bandit#@bandit.labs...` host. Use the password that you obtained in the previous level:

So `ssh bandit1@bandit.labs.overthewire.org -p 2220` and, when prompted for the password, enter `boJ9jbbUNNfktd78OOpsqOltutMc3MY1` which we found in `readme` in level0.


Great; we're logged into `bandit1`. Let's have a look around:

```console
bandit1@bandit:~$ ls -a
-  .  ..  .bash_logout  .bashrc  .profile
-  
bandit1@bandit:~$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```


## level_2 -> 3

The password for the next level can be found in a file called `spaces in this filename` in the home dir:

```console
bandit2@bandit:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  spaces in this filename

bandit2@bandit:~$ cat "spaces in this filename"
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```



## level_3 -> 4
The password for the next level is stored in a hidden file in the `inhere` directory.

```console
bandit3@bandit:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  inhere

bandit3@bandit:~$ cd inhere/

bandit3@bandit:~/inhere$ ls

bandit3@bandit:~/inhere$ ls -al
total 12
drwxr-xr-x 2 root    root    4096 Dec 28 14:34 .
drwxr-xr-x 3 root    root    4096 Dec 28 14:34 ..
-rw-r----- 1 bandit4 bandit3   33 Dec 28 14:34 .hidden

bandit3@bandit:~/inhere$ cat .hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

## level_4 -> 5
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

```
bandit4@bandit:~$ ls
inhere

bandit4@bandit:~$ cd inhere

bandit4@bandit:~/inhere$ ls
-file00  -file02  -file04  -file06  -file08
-file01  -file03  -file05  -file07  -file09

bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data

bandit4@bandit:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

## level_5 -> 6

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

 - human-readable
 - 1033 bytes in size
 - not executable

```console
bandit5@bandit:~$ ls
inhere

bandit5@bandit:~$ cd inhere/

bandit5@bandit:~/inhere$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17

bandit5@bandit:~/inhere$ find -type f -size 1033c
./maybehere07/.file2

bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

## level_6 -> 7

The password for the next level is stored somewhere on the server and has all of the following properties:

 - owned by user bandit7
 - owned by group bandit6
 - 33 bytes in size

```console
bandit6@bandit:~$ ls -al
total 20
drwxr-xr-x  2 root root 4096 Dec 28 14:34 .
drwxr-xr-x 29 root root 4096 Dec 28 14:34 ..
-rw-r--r--  1 root root  220 Sep  1  2015 .bash_logout
-rw-r--r--  1 root root 3771 Sep  1  2015 .bashrc
-rw-r--r--  1 root root  655 Jun 24  2016 .profile

bandit6@bandit:~$ cd ..

bandit6@bandit:/home$ ls
bandit0   bandit12  bandit16  bandit2   bandit23  bandit3  bandit7
bandit1   bandit13  bandit17  bandit20  bandit24  bandit4  bandit8
bandit10  bandit14  bandit18  bandit21  bandit25  bandit5  bandit9
bandit11  bandit15  bandit19  bandit22  bandit26  bandit6

bandit6@bandit:/home$ find / -user bandit7 -group bandit6 -size 33c
find: '/etc/ssl/private': Permission denied
find: '/etc/polkit-1/localauthority': Permission denied
find: '/run/lxcfs': Permission denied
find: '/run/user/11002': Permission denied
find: '/run/user/11001': Permission denied
find: '/run/user/11010': Permission denied
find: '/run/user/11022': Permission denied
find: '/run/user/11012': Permission denied
find: '/run/user/11003': Permission denied
find: '/run/user/11024': Permission denied
find: '/run/user/11020': Permission denied
find: '/run/user/11015': Permission denied
[...]
```

A big list of results; let's try to find just the relevant result by excluding the Permission denied results:

```console
bandit6@bandit:/home$ find / -user bandit7 -group bandit6 -size 33c 2>&1 | grep -v "Permission denied"
/var/lib/dpkg/info/bandit7.password
find: '/proc/31445/task/31445/fd/6': No such file or directory
find: '/proc/31445/task/31445/fdinfo/6': No such file or directory
find: '/proc/31445/fd/5': No such file or directory
find: '/proc/31445/fdinfo/5': No such file or directory

bandit6@bandit:/home$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs

```



## level_7 -> 8

The password for the next level is stored in the file data.txt next to the word millionth

```console
bandit7@bandit:~$ ls -al
total 4108
drwxr-xr-x  2 root    root       4096 Dec 28 14:34 .
drwxr-xr-x 29 root    root       4096 Dec 28 14:34 ..
-rw-r--r--  1 root    root        220 Sep  1  2015 .bash_logout
-rw-r--r--  1 root    root       3771 Sep  1  2015 .bashrc
-rw-r--r--  1 root    root        655 Jun 24  2016 .profile
-rw-r-----  1 bandit8 bandit7 4184396 Dec 28 14:34 data.txt
bandit7@bandit:~$ grep -o '.\{0,20\}millionth.\{0,40\}' data.txt
millionth   cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```


## level_8 -> 9
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once


```console
bandit8@bandit:~$ sort data.txt | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```


## level_9 -> 10

The password for the next level is stored in the file data.txt in one of the few human-readable strings, beginning with several ‘=’ characters.

```console
bandit9@bandit:~$strings data.txt
[...]
Iu)d9[
9=!/"
.+,1u
/g;.9
========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
}r@V
)ng3S
s<aF
H3XB
De$3n
[...]
```

## level_10 -> 11
The password for the next level is stored in the file data.txt, which contains base64 encoded data

```
bandit10@bandit:~$ base64 -d data.txt
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

## level_11 -> 12
**My comment: ROT13 - "rotate by 13 places" - is a simple Caesar / substitution cipher in which the first letter of the alphabet is shifted to the 13th letter of the alphabet, i.e., `A` becomes `N`, `B` becomes `O`, etc.


The instructions for this level read as follows: 
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

```
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

## level_12 -> 13

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed.

When we log into the `bandit` host it always tells us that we can create a tmp directory to use as a scratch space. Since we'll be doing a lot of decompressing, let's create our temporary directory:

```
bandit12@bandit:~$ mktemp -d
/tmp/tmp.iyWHebg3Ji
```


```console
bandit12@bandit:/tmp/tmp.iyWHebg3Ji$ zcat dat.bin | bzcat | zcat | tar xO | tar xO | bzcat | file -
/dev/stdin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.iyWHebg3Ji$ zcat dat.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO |file -
/dev/stdin: gzip compressed data, was "data9.bin", last modified: Thu Dec 28 13:34:36 2017, max compression, from Unix
bandit12@bandit:/tmp/tmp.iyWHebg3Ji$ zcat dat.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat | file -
/dev/stdin: ASCII text
bandit12@bandit:/tmp/tmp.iyWHebg3Ji$ zcat dat.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
bandit12@bandit:/tmp/tmp.iyWHebg3Ji$
```


## level_13 -> 14

The instructions which tell us to look in `/etc/bandit_pass/bandit14 ` which can only be read by user `bandit14`. 

Commands you _may_ need to solve this level include `ssh`, `telnet`, `nc`, `openssl`, `s_client`, `nmap`.

```console
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

## level_14 -> 15

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

Commands you _may_ need to solve this level include `ssh`, `telnet`, `nc`, `openssl`, `s_client`, `nmap`.


```console
bandit14@bandit:~$ telnet localhost 30000
Trying ::1...
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr

Connection closed by foreign host.
bandit14@bandit:~$
```

## level_15 -> 16

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command.

Commands you _may_ need to solve this level include `ssh`, `telnet`, `nc`, `openssl`, `s_client`, `nmap`.

Check out open [SSL cookbook](https://www.feistyduck.com/library/openssl-cookbook/online/ch-testing-with-openssl.html) for a nice write-up on SSL services if you need a refresher.


```console
bandit15@bandit:~$ openssl s_client -connect localhost:30001 -ign_eof
CONNECTED(00000003)
depth=0 CN = bandit
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = bandit
verify return:1
---
Certificate chain
 0 s:/CN=bandit
   i:/CN=bandit
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICsjCCAZqgAwIBAgIJAKZI1xYeoXFuMA0GCSqGSIb3DQEBCwUAMBExDzANBgNV
BAMMBmJhbmRpdDAeFw0xNzEyMjgxMzIzNDBaFw0yNzEyMjYxMzIzNDBaMBExDzAN
BgNVBAMMBmJhbmRpdDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAOcX
ruVcnQUBeHJeNpSYayQExCJmcHzSCktnOnF/H4efWzxvLRWt5z4gYaKvTC9ixLrb
K7a255GEaUbP/NVFpB/sn56uJc1ijz8u0hWQ3DwVe5ZrHUkNzAuvC2OeQgh2HanV
5LwB1nmRZn90PG1puKxktMjXsGY7f9Yvx1/yVnZqu2Ev2uDA0RXij/T+hEqgDMI7
y4ZFmuYD8z4b2kAUwj7RHh9LUKXKQlO+Pn8hchdR/4IK+Xc4+GFOin0XdQdUJaBD
8quOUma424ejF5aB6QCSE82MmHlLBO2tzC9yKv8L8w+fUeQFECH1WfPC56GcAq3U
IvgdjGrU/7EKN5XkONcCAwEAAaMNMAswCQYDVR0TBAIwADANBgkqhkiG9w0BAQsF
AAOCAQEAnrOty7WAOpDGhuu0V8FqPoKNwFrqGuQCTeqhQ9LP0bFNhuH34pZ0JFsH
L+Y/q4Um7+66mNJUFpMDykm51xLY2Y4oDNCzugy+fm5Q0EWKRwrq+hIM+5hs0RdC
nARP+719ddmUiXF7r7IVP2gK+xqpa8+YcYnLuoXEtpKkrrQCCUiqabltU5yRMR77
3wqB54txrB4IhwnXqpO23kTuRNrkG+JqDUkaVpvct+FAdT3PODMONP/oHII3SH9i
ar/rI9k+4hjlg4NqOoduxX9M+iLJ0Zgj6HAg3EQVn4NHsgmuTgmknbhqTU3o4IwB
XFnxdxVy0ImGYtvmnZDQCGivDok6jA==
-----END CERTIFICATE-----
subject=/CN=bandit
issuer=/CN=bandit
---
No client certificate CA names sent
---
SSL handshake has read 1015 bytes and written 631 bytes
---
New, TLSv1/SSLv3, Cipher is AES128-SHA
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1
    Cipher    : AES128-SHA
    Session-ID: DE3F72FC96136281A642DA83F56427208BE1C97B3FD3EB756BCBCEBE2CDFDD0B
    Session-ID-ctx:
    Master-Key: 92E520628D78191686B08C1D296D21C4557458A77BBB6A0D1D03ED265F32E9CDBF70DC6AABC7E2DF6EAA95856190152C
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 08 f0 15 a5 d6 6f a0 e8-06 d6 bb a4 0c 33 eb 04   .....o.......3..
    0010 - b1 91 ac 3b 26 2c b1 95-31 e0 4d ce 97 d4 a7 d4   ...;&,..1.M.....
    0020 - c4 d3 38 36 e1 ce 5c 9e-c3 0c c8 b0 83 31 cf 92   ..86..\......1..
    0030 - 50 c2 6c d6 fb cd de 3b-a7 d1 31 d7 e0 72 9d 9a   P.l....;..1..r..
    0040 - d0 81 ed a6 ef 90 1c a1-80 9a cc 0f b5 21 53 6a   .............!Sj
    0050 - cb a5 ef 12 17 84 6a 0e-0e a6 fc c4 dc 10 84 39   ......j........9
    0060 - 0f 55 0e af a6 de b2 ed-bc b0 86 97 5c 49 5e 59   .U..........\I^Y
    0070 - 33 e4 7a 70 30 39 40 65-15 af f5 d6 e6 3e 8c 39   3.zp09@e.....>.9
    0080 - e0 b1 2e 53 a6 db c4 22-53 4e a7 ab c7 1c bc 50   ...S..."SN.....P
    0090 - 0a 49 03 d0 d1 20 d9 18-e0 03 3b 7e c6 c2 04 e4   .I... ....;~....

    Start Time: 1524612398
    Timeout   : 300 (sec)
    Verify return code: 18 (self signed certificate)
---
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd

closed
bandit15@bandit:~$
```


## level_16 -> 17

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.


This command never completed:
```console
bandit16@bandit:~$ nmap -A -T4 -p 31000-32000 localhost

Starting Nmap 7.01 ( https://nmap.org ) at 2018-04-28 18:43 CEST
``` 
... so we remove the flags (except for the port number flags) and try again:

```console
bandit16@bandit:~$ nmap -p 31000-32000 localhost

Starting Nmap 7.01 ( https://nmap.org ) at 2018-04-28 18:47 CEST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00019s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 996 closed ports
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.07 seconds
```

Also, this command below doesn't really help us that much:
```
bandit16@bandit:~$ for i in $(echo "127.0.0.1"|tr "," "\n"); do echo -e "31046\n31518\n31691\n31790\n31960" | xargs -i nc -w 1 -znv $i {}; done
Connection to 127.0.0.1 31046 port [tcp/*] succeeded!
Connection to 127.0.0.1 31518 port [tcp/*] succeeded!
Connection to 127.0.0.1 31691 port [tcp/*] succeeded!
Connection to 127.0.0.1 31790 port [tcp/*] succeeded!
Connection to 127.0.0.1 31960 port [tcp/*] succeeded!
```

```
bandit16@bandit:~$ nmap -p 30999-32001 localhost

Starting Nmap 7.01 ( https://nmap.org ) at 2018-04-28 18:50 CEST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00030s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 998 closed ports
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

bandit16@bandit:~$ mktemp -d
/tmp/tmp.9n4m7UmJMj

bandit16@bandit:~$ echo "" | openssl s_client -connect localhost:31960
CONNECTED(00000003)
140737354045080:error:140770FC:SSL routines:SSL23_GET_SERVER_HELLO:unknown protocol:s23_clnt.c:794:
---
no peer certificate available
---
No client certificate CA names sent
---
SSL handshake has read 7 bytes and written 305 bytes
---
New, (NONE), Cipher is (NONE)
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : 0000
    Session-ID:
    Session-ID-ctx:
    Master-Key:
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    Start Time: 1524934751
    Timeout   : 300 (sec)
    Verify return code: 0 (ok)
---
bandit16@bandit:~$ echo "" | openssl s_client -connect localhost:31790
CONNECTED(00000003)
depth=0 CN = bandit
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = bandit
verify return:1
---
Certificate chain
 0 s:/CN=bandit
   i:/CN=bandit
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICsjCCAZqgAwIBAgIJAKZI1xYeoXFuMA0GCSqGSIb3DQEBCwUAMBExDzANBgNV
BAMMBmJhbmRpdDAeFw0xNzEyMjgxMzIzNDBaFw0yNzEyMjYxMzIzNDBaMBExDzAN
BgNVBAMMBmJhbmRpdDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAOcX
ruVcnQUBeHJeNpSYayQExCJmcHzSCktnOnF/H4efWzxvLRWt5z4gYaKvTC9ixLrb
K7a255GEaUbP/NVFpB/sn56uJc1ijz8u0hWQ3DwVe5ZrHUkNzAuvC2OeQgh2HanV
5LwB1nmRZn90PG1puKxktMjXsGY7f9Yvx1/yVnZqu2Ev2uDA0RXij/T+hEqgDMI7
y4ZFmuYD8z4b2kAUwj7RHh9LUKXKQlO+Pn8hchdR/4IK+Xc4+GFOin0XdQdUJaBD
8quOUma424ejF5aB6QCSE82MmHlLBO2tzC9yKv8L8w+fUeQFECH1WfPC56GcAq3U
IvgdjGrU/7EKN5XkONcCAwEAAaMNMAswCQYDVR0TBAIwADANBgkqhkiG9w0BAQsF
AAOCAQEAnrOty7WAOpDGhuu0V8FqPoKNwFrqGuQCTeqhQ9LP0bFNhuH34pZ0JFsH
L+Y/q4Um7+66mNJUFpMDykm51xLY2Y4oDNCzugy+fm5Q0EWKRwrq+hIM+5hs0RdC
nARP+719ddmUiXF7r7IVP2gK+xqpa8+YcYnLuoXEtpKkrrQCCUiqabltU5yRMR77
3wqB54txrB4IhwnXqpO23kTuRNrkG+JqDUkaVpvct+FAdT3PODMONP/oHII3SH9i
ar/rI9k+4hjlg4NqOoduxX9M+iLJ0Zgj6HAg3EQVn4NHsgmuTgmknbhqTU3o4IwB
XFnxdxVy0ImGYtvmnZDQCGivDok6jA==
-----END CERTIFICATE-----
subject=/CN=bandit
issuer=/CN=bandit
---
No client certificate CA names sent
---
SSL handshake has read 1015 bytes and written 631 bytes
---
New, TLSv1/SSLv3, Cipher is AES128-SHA
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1
    Cipher    : AES128-SHA
    Session-ID: 4450C44EA141C37FF605CDAA05919BC71C0D3CEE5A42191B6A41713C392E10F2
    Session-ID-ctx:
    Master-Key: 910EBF7A2AD2B2100C574515CE66DB0BEB07030DF80F6519D365C55D1C63EB696050AD3045F7BA9AFCEDDD9FD01D8333
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 9a b6 c1 e5 3e 9c 51 03-45 ba c9 c1 cc d7 23 80   ....>.Q.E.....#.
    0010 - 71 5e 7a 83 f4 e6 f0 d7-92 84 09 6e b8 1f f3 4b   q^z........n...K
    0020 - 4c 5d a2 16 cb fc 28 93-af 06 01 d2 44 14 ef a8   L]....(.....D...
    0030 - 5c ae 74 1a 08 84 82 7e-95 be 9e fc 1c c6 7c f4   \.t....~......|.
    0040 - 01 ef a9 14 c2 e1 b2 37-4c 96 0c 1b 63 f4 1b de   .......7L...c...
    0050 - 43 93 c5 10 57 59 2c 1f-56 0d cc a1 8e 0d 86 67   C...WY,.V......g
    0060 - 05 e7 4a 03 23 02 47 0c-be 7a 05 48 70 1a 07 3f   ..J.#.G..z.Hp..?
    0070 - d6 ac c7 a0 d0 da ff 05-fe 6f 61 d9 2e 0c be 3f   .........oa....?
    0080 - bd cd 77 9b f1 82 f4 6f-ba 48 49 c2 2b 19 3f 3e   ..w....o.HI.+.?>
    0090 - 47 34 05 bf 6b 3d 4e aa-6b 4f 99 8c a1 9e 1d 9a   G4..k=N.kO......

    Start Time: 1524934774
    Timeout   : 300 (sec)
    Verify return code: 18 (self signed certificate)
---
DONE
```
**okay** so the port we want to investigate further is 31790.

Took a break. Connection closed. Came back and had to `ssh` in again...

```console
bandit16@bandit:~$ mktemp -d
/tmp/tmp.PUf5umuysl`

$ cat level16.txt | openssl s_client -connect localhost:31790
```
```
bandit16@bandit:/$ cd //tmp/tmp.PUf5umuysl
bandit16@bandit://tmp/tmp.PUf5umuysl$ ls
bandit16@bandit://tmp/tmp.PUf5umuysl$ touch bandit17.txt
bandit16@bandit://tmp/tmp.PUf5umuysl$ nano bandit17.txt
Unable to create directory /home/bandit16/.nano: Permission denied
It is required for saving/loading search history or cursor positions.

Press Enter to continue

bandit16@bandit://tmp/tmp.PUf5umuysl$ ls
bandit17.txt
bandit16@bandit://tmp/tmp.PUf5umuysl$ chmod 600 bandit17.txt
bandit16@bandit://tmp/tmp.PUf5umuysl$ ssh bandit17@localhost -i ./bandit17.txt
Could not create directory '/home/bandit16/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit16/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

      ,----..            ,----,          .---.
     /   /   \         ,/   .`|         /. ./|
    /   .     :      ,`   .'  :     .--'.  ' ;
   .   /   ;.  \   ;    ;     /    /__./ \ : |
  .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
  ;   |  ; \ ; | |    :     | /___/ \ |    ' '
  |   :  | ; | ' ;    |.';  ; ;   \  \;      :
  .   |  ' ' ' : `----'  |  |  \   ;  `      |
  '   ;  \; /  |     '   :  ;   .   \    .\  ;
   \   \  ',  /      |   |  '    \   \   ' \ |
    ;   :    /       '   :  |     :   '  |--"
     \   \ .'        ;   |.'       \   \ ;
  www. `---` ver     '---' he       '---" ire.org


Welcome to OverTheWire!


--[ More information ]--

  For more information regarding individual wargames, visit
  http://www.overthewire.org/wargames/

  For support, questions or comments, contact us through IRC on
  irc.overthewire.org #wargames.

  Enjoy your stay!

bandit17@bandit:~$
```

## level_17 -> 18

There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new.

```console
bandit17@bandit:~$ ls
passwords.new  passwords.old

bandit17@bandit:~$ diff -C 3 passwords.old passwords.new
*** passwords.old   Thu Dec 28 14:34:40 2017
--- passwords.new   Thu Dec 28 14:34:40 2017
***************
*** 39,45 ****
  kvKr7iaqGW5CKUftWk42VS484t604V4g
  pXBXbholP8jghELrQEx34Iwf5D9aErSf
  eDeZU3HfyLEXjHHl8JFYNHyOkQg0RKFx
! 6vcSC74ROI95NqkKaeEC2ABVMDX9TyUr
  EUQQhloPsGyLXbxs97kiw5jt2h5Ij7Bc
  tADigBLkc3nqnaOpRAhjdVore9I7L80V
  EEAw8isg6JgVWrwxsaUS8ZpoydJuAX1u
--- 39,45 ----
  kvKr7iaqGW5CKUftWk42VS484t604V4g
  pXBXbholP8jghELrQEx34Iwf5D9aErSf
  eDeZU3HfyLEXjHHl8JFYNHyOkQg0RKFx
! kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
  EUQQhloPsGyLXbxs97kiw5jt2h5Ij7Bc
  tADigBLkc3nqnaOpRAhjdVore9I7L80V
  EEAw8isg6JgVWrwxsaUS8ZpoydJuAX1u
bandit17@bandit:~$
```

And now we're able to `ssh` into level 18:
```
bandit17@bandit:~$ ssh bandit18@localhost
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit17/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for '/home/bandit17/.ssh/id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/home/bandit17/.ssh/id_rsa": bad permissions
bandit18@localhost's password:

      ,----..            ,----,          .---.
     /   /   \         ,/   .`|         /. ./|
    /   .     :      ,`   .'  :     .--'.  ' ;
   .   /   ;.  \   ;    ;     /    /__./ \ : |
  .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
  ;   |  ; \ ; | |    :     | /___/ \ |    ' '
  |   :  | ; | ' ;    |.';  ; ;   \  \;      :
  .   |  ' ' ' : `----'  |  |  \   ;  `      |
  '   ;  \; /  |     '   :  ;   .   \    .\  ;
   \   \  ',  /      |   |  '    \   \   ' \ |
    ;   :    /       '   :  |     :   '  |--"
     \   \ .'        ;   |.'       \   \ ;
  www. `---` ver     '---' he       '---" ire.org


Welcome to OverTheWire!

If you find any problems, please report them to Steven or morla on
irc.overthewire.org.
```

## level_18 -> 19

The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

```console
bandit17@bandit:~$ ssh bandit18@localhost ls
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit17/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for '/home/bandit17/.ssh/id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/home/bandit17/.ssh/id_rsa": bad permissions
bandit18@localhost's password:
readme
```
Okay, there's a file called `readme` that we should examine using `cat`.

```console
bandit17@bandit:/tmp$ ssh bandit18@localhost cat readme
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit17/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for '/home/bandit17/.ssh/id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/home/bandit17/.ssh/id_rsa": bad permissions
bandit18@localhost's password:
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

So then to get to the next level, we
`ssh bandit19@localhost` and use the password `IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x`

## level_19 -> 20

To gain access to the next level, you should use the setuid binary in the home directory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

```console
bandit19@bandit:~$ ls -al
total 28
drwxr-xr-x  2 root     root     4096 Dec 28 14:34 .
drwxr-xr-x 29 root     root     4096 Dec 28 14:34 ..
-rw-r--r--  1 root     root      220 Sep  1  2015 .bash_logout
-rw-r--r--  1 root     root     3771 Sep  1  2015 .bashrc
-rw-r--r--  1 root     root      655 Jun 24  2016 .profile
-rwsr-x---  1 bandit20 bandit19 7408 Dec 28 14:34 bandit20-do
```
Hrm, the `bandit20-do` binary is owned by `bandit20`, so we (we're `bandit19` probably can't run this... But let's try anyway)


```
bandit19@bandit:~$ stat -c "%a %A" ./bandit20-do
4750 -rwsr-x---
```

[This page has a nice overview of `setuid`](https://major.io/2007/02/13/chmod-and-the-mysterious-first-octet/)

```
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
```
The instructions on OTW told us that the password lives in `bandit_pass/bandit20` per usual: `"The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary."`
```
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

## level_20 -> 21

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

Commands you may want to use: `ssh`,`nc`, `bash`, `screen`, `tmux`, *nix job control such (`bg`,`fg`, etc.)

Let's `ssh` into level 20 to start out with:
`ssh bandit20@bandit.labs.overthewire.org -p 2220`
And then our password:
`GbKksEFF4yrVs6il55v6gwY5aVje5f0j`

Let's see what's in our home directory:
```
bandit20@bandit:~$ ll
total 28
drwxr-xr-x  2 root     root     4096 Dec 28 14:34 ./
drwxr-xr-x 29 root     root     4096 Dec 28 14:34 ../
-rw-r--r--  1 root     root      220 Sep  1  2015 .bash_logout
-rw-r--r--  1 root     root     3771 Sep  1  2015 .bashrc
-rw-r--r--  1 root     root      655 Jun 24  2016 .profile
-rwsr-x---  1 bandit21 bandit20 8044 Dec 28 14:34 suconnect*
```
This `suconnect` file is what we're looking for. `bandit21` is the owner and `bandit20` is the group.


```
bandit20@bandit:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
```
We need to be able to listen on a given port **and then** also fire up `suconnect` (on the same port) and listen for the response which is the password for the next level. Using `bg` we can run a given command in the background. Simply run your desired command, press `ctrl+z` (`^Z` is how it appears in the shell / below ), and then enter `bg`. Now your commandline is free to accept another command, namely `./suconnect [samePortNumberAsYouUsedWhenStartingNetcat]`:

```
bandit20@bandit:~$ nc -l 1337 < /etc/bandit_pass/bandit20
^Z
[1]+  Stopped                 nc -l 1337 < /etc/bandit_pass/bandit20
bandit20@bandit:~$ bg
[1]+ nc -l 1337 < /etc/bandit_pass/bandit20 &
bandit20@bandit:~$ ./suconnect 1337
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
[1]+  Done                    nc -l 1337 < /etc/bandit_pass/bandit20
```
Great! We've got our password / flag for this level!

## level_21 -> 22

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in `/etc/cron.d/`` for the configuration and see what command is being executed.

```console
bandit21@bandit:/$ cd /etc/cron.d/
bandit21@bandit:/etc/cron.d$ ls
cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  popularity-contest
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
bandit21@bandit:/etc/cron.d$
```

## level_22 -> 23

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

This level is basically about looking at other people's shell scripts and figuring out what those shell scripts are doing. Let's get crackin':

```console
bandit22@bandit:~$ cd /etc/cron.d
bandit22@bandit:/etc/cron.d$ ls
cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  popularity-contest
bandit22@bandit:/etc/cron.d$ ls -al
total 28
drwxr-xr-x   2 root root 4096 Dec 28 14:34 .
drwxr-xr-x 100 root root 4096 Mar 12 09:51 ..
-rw-r--r--   1 root root  102 Apr  5  2016 .placeholder
-rw-r--r--   1 root root  120 Dec 28 14:34 cronjob_bandit22
-rw-r--r--   1 root root  122 Dec 28 14:34 cronjob_bandit23
-rw-r--r--   1 root root  120 Dec 28 14:34 cronjob_bandit24
-rw-r--r--   1 root root  190 Oct 31 13:21 popularity-contest
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
Great! We found the shell script that is doing something! It looks like it's copying the password file from `/etc/bandit_pass/$myname` to `/tmp/$mytarget`.

Let's see what is in the directory (a MD5 hash) by `cat`ting the `/tmp/8ca[...] directory.

```console
bandit22@bandit:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
bandit22@bandit:/etc/cron.d$
```

Try sshing into `bandit23`: `dataJanitor-s-MacBookPro:~ datajanitor$ ssh bandit23@bandit.labs.overthewire.org -p 2220` with the password:  `jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n` and - SUCCESS! - it works. Moving on to the next level...

## level_23 -> 24

Here are the level notes:

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…
---

Let's get started:
`ssh` into the level23 box:
`ssh bandit23@bandit.labs.overthewire.org -p 2220` using the password
`jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n`.

Navigate back to the `cron.d` directory and look inside:
```console
bandit23@bandit://etc/cron.d$ ls
cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  popularity-contest
```

Looking inside this level's cronjob we see an `echo` saying that `cronjob_bandit24.sh` executes and then deletes all scripts in `/var/spool/$myname`
```console
bandit23@bandit://etc/cron.d$ cat cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit://etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
    echo "Handling $i"
    timeout -s 9 60 ./$i
    rm -f ./$i
    fi
done
```

Let's make our shell script and try to leverage the fact that all scripts in `/var/spool/$myname` are run:

Make our temp directory to store the shell script
`mkdir /tmp/ap1212`
`cd /tmp/ap1212`
`touch opensesame.sh`
`nano opensesame.sh`

Let's add the following to `opensesame.sh`:
```
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/ap1212/pass.txt
```

which is the same thing that we did a few levels ago by writing a password to another file so that we could view it.

Save and exit and then change the permissions on your shell script so that you can execute it:

`chmod 777 opensesame.sh`

and don't forget to let yourself write to your directory:
`chmod 777 /tmp/ap1212/ `

Now, copy your shell script into the `/var/spool/` directory so that the shell script will be run by the cron job:

`cp opensesame.sh /var/spool/bandit24`


It'll take a few minutes before the cron job will run again, but try `ls`ing to see if your `pass.txt` has appeared:
```console
bandit23@bandit:/tmp/ap1212$ ls
opensesame.sh  pass.txt
```

Great! Let's see what's inside:
```console
bandit23@bandit:/tmp/ap1212$ cat pass.txt
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```
