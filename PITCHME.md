# PHPTRACE

A tracing and troubleshooting tool for PHP scripts.

---

### Agenda 

- Introduction for phptrace
- Install and verify 
- Example for tracing PHP runtime

---

### What is phptrace

- phptrace is an open source tool developed by Qihoo 360 team.
- Can track PHP executing process.
- Can print PHP stack, can debug loop issue.

---

### Install and verify install succ

- Git repo: https://github.com/Qihoo360/phptrace
  - Install it from source or with package manager (Centos: remi repo yum install php-pecl-trace)
  - Enable the module from php.ini 
- We provide the tool within Projecx container.

```
#Verify it installed succ:
php -r 'for ($i = 0; $i < 20; $i++) usleep(500000);' &     
phptrace -p $!                                            
```

---

### Usage - trace PHP runtime

- Login to qa.liwenbianji.cn and get into docker container.
- Demo

```
php -r 'for ($i = 0; $i < 20; $i++) usleep(500000);' &     # We start a PHP run in background. usleep is a function to simulate a block in PHP, so we can see it run:
phptrace -p $!                                             # $! means that process id, we need to trace that special progress id. this can be found with linux command 'top'
phptrace -p all -f type=function,content=mail              # Trace all mail related function call on all php-fpm process
```

---

### Usage - print PHP stack while process block.

1. Login to qa.author-path.com
2. Open two CLI.
3. On CLI one run: 
```
php example.php                        #example.php: https://raw.githubusercontent.com/Qihoo360/phptrace/master/example.php
```
4. On CLI two, find the PID of above progres, it also display the process id already.
```
ps -ef | grep example
```
5. On CLI two, run phptrace and at the sametime switch to CLI one and press enter to let the PHP run:
```
On CLI two: phptrace status -p <process number>
On CLI one: press enter

**Note**: the timeout for php status is 2 seconds, it assume it can attach any php runtime within 2 seconds. if not - it will exist with timeout.

---

### Usage - track and filter function

- Login to qa.liwenbianji.cn
- Demo switch to 

