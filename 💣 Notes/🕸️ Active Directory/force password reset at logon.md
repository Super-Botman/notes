# force password reset at logon

```powershell
Set-ADUser -ChangePasswordAtLogon $true -Identity USER -Verbose
```