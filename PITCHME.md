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
- Can print PHP stack and debug loop issue.

---

#### Install and verify install succ

- Git repo: https://github.com/Qihoo360/phptrace
  - Install it from source or with package manager (Centos: remi repo yum install php-pecl-trace)
  - Enable the module from php.ini 
- We provide it within Projecx docker container.

```
#Verify installed succ:
php -r 'for ($i = 0; $i < 20; $i++) usleep(500000);' &     
phptrace -p $!                                            
```

---

#### Usage - trace PHP runtime

- Login to qa.liwenbianji.cn and attach to docker container.
```
docker exec -it projectx-ops-422-20180622_152400 /bin/bash
```
- Demo

```
# Below we start a PHP process in background. usleep is a function to simulate a block in PHP, so we can see the run progress:
php -r 'for ($i = 0; $i < 20; $i++) usleep(500000);' & 
# Below we run phptrace to the above php, $! means that process id, for other php run, we can find php running progress with linux command 'top'
phptrace -p $! 
# Below we trace all mail related function call on all php-fpm process, then access a mail related page, it will output any function have 'mail' keywords.
phptrace -p all -f type=function,content=mail  
```

---

#### Usage - print PHP stack while process block.

- Login to qa.liwenbianji.cn and open another CLI attached to container.

```
# Below we run a example.php: https://raw.githubusercontent.com/Qihoo360/phptrace/master/example.php
php example.php  
# It will display the PID of the progress, but usually we need to find the PID of above progres with linux command top.
# On the other CLI, run below command and immedately switch to php example.php CLI and press enter to continue the progress run.
phptrace status -p <process number>

```
- Note: the timeout for php status is 2 seconds, if it have not found any php logic, it will timeout and exit with error.

---

### Questions & Answer

- Q/A
- Suggestions.

