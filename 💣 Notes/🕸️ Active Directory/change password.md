# change password

```powershell
Set-ADAccountPassword USER -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
```