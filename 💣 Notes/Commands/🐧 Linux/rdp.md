# rdp

connect to a windows target using `xfreerdp`:

```bash
IP=<IP>
USER=<USER>
PASSWD=<PASSWD>

xfreerdp /v:$IP /u:$USEE /p:$PASSWD +clipboard /dynamic-resolution /drive:/usr/share/windows-resources,share
```