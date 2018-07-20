# PHPTRACE

A tracing and troubleshooting tool for PHP scripts.

---

### What is phptrace

- phptrace is an open source tool developed by Qihoo 360 team.
- It can be helpful to identify PHP blocking related issue.

---

### Install and verify install succ

- Git repo: https://github.com/Qihoo360/phptrace
  - Install it from source or with package manager (Yum: remi repo)
  - Enable the module from php.ini 
  - php -r 'for ($i = 0; $i < 20; $i++) usleep(500000);' &     
  - phptrace -p $!                                            
- We will provide it on our QA and Live server.

---

### Usage - trace PHP runtime

- Login to qa.author-path.com
- Demo Run:
  - php -r 'for ($i = 0; $i < 20; $i++) usleep(500000);' &     # We start a PHP run in background. usleep is a function to simulate a block in PHP, so we can see.
  - phptrace -p $!                                             # $! means that process id, this means use phptrace to trace the process id.

---

### Usage - print PHP stack

- Login to qa.author-path.com
- Demo Run:
  - Open two CLI.
  - On one CLI, run: php /tmp/example.php                  # We start a PHP run in background. usleep is a function to simplyly simulate a block in PHP, so we can see.
  - On the other CLI, run: phptrace status -p $!           # $! means that process id, this means use phptrace to trace the process id.

---

### Usage - track and filter function

- Login to qa.liwenbianji.cn
- Demo switch to 

