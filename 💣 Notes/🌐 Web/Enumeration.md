# Enumeration

## Enum routes

### gobuster

```bash
gobuster dir -w /usr/share/wordlists/SecLists-master/Discovery/Web-Content/directory-list-2.3-big.txt -u <IP>
```

### dirsearch

```bash
dirsearch -u <IP> -e php,html,js
```

## Enum Vhosts

```bash
gobuster vhost -w /usr/share/wordlists/SecLists-master/Discovery/DNS/subdomains-top1million-20000.txt -u <IP>
```