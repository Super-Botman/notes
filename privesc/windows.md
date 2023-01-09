# Table of content

```{r load_packages, message=FALSE, warning=FALSE, include=FALSE}
library(fontawesome)
```

- [Table of content](#table-of-content)
- [return to index](INDEX.md)
  - [manual](#manual)
    - [Unattended Windows Installations](#unattended-windows-installations)
    - [Powershell History](#powershell-history)
    - [Saved Windows Credentials](#saved-windows-credentials)
    - [IIS Configuration](#iis-configuration)
    - [Retrieve Credentials PuTTY](#retrieve-credentials-putty)
    - [Scheduled Tasks](#scheduled-tasks)
    - [check permissions of a file](#check-permissions-of-a-file)

## manual

### Unattended Windows Installations

you can find some logins in this dir:
    - C:\Unattend.xml
    - C:\Windows\Panther\Unattend.xml
    - C:\Windows\Panther\Unattend\Unattend.xml
    - C:\Windows\system32\sysprep.inf
    - C:\Windows\system32\sysprep\sysprep.xml

[:arrow_up:](#)
  
### Powershell History

you can also check the cmd history using this commands:

- cmd.exe :

```cmd
type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```

- powershell.exe :

```cmd
type $Env:userprofile\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```
[:arrow_up:](#)

### Saved Windows Credentials

this list saved credentials :

```cmd
cmdkey /list
```

change of user:

```cmd
runas /savecred /user:admin cmd.exe
```
[:arrow_up:](#)

### IIS Configuration

you can find config file at this locations:

    - C:\inetpub\wwwroot\web.config
    - C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config

and you can use this command:

```cmd
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
```
[:arrow_up:](#)

### Retrieve Credentials PuTTY

```cmd
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```
[:arrow_up:](#)

### Scheduled Tasks

get scheduled tasks set:

```cmd
schtasks /query /tn vulntask /fo list /v
```
[:arrow_up:](#)

### check permissions of a file

```cmd
icacls c:\tasks\schtask.bat
```
[:arrow_up:](#)
