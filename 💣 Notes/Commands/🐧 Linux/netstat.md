# netstat

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