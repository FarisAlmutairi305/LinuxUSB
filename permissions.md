# File & Folder Permissions (Ubuntu Server)

This file contains **commands to view, modify, and manage permissions** on Linux/Ubuntu Server.  
Reference only — commands are **not executed automatically**.  
Works in terminal with nano, cat, or less.

---

## View Permissions

List permissions of files/folders:
```
ls -l
```

List permissions recursively:
```
ls -lR
```

Show file or folder with numeric permissions:
```
stat filename
```

Check ACL (Access Control List) if used:
```
getfacl filename
```

---

## Change Permissions

### Using `chmod`

Change permissions using symbolic notation:
```
chmod u+rwx,g+rx,o+r filename
```
- `u` = user (owner)  
- `g` = group  
- `o` = others  

Remove permissions:
```
chmod o-rwx filename
```

Change permissions using numeric notation:
```
chmod 755 filename
```
- 7 = read/write/execute  
- 6 = read/write  
- 5 = read/execute  
- 4 = read only  

Apply permissions recursively:
```
chmod -R 755 foldername
```

---

### Using `chown` (Change Owner)

Change owner:
```
sudo chown user filename
```

Change owner and group:
```
sudo chown user:group filename
```

Change recursively:
```
sudo chown -R user:group foldername
```

---

### Using `chgrp` (Change Group Only)

```
sudo chgrp groupname filename
sudo chgrp -R groupname foldername
```

---

## Common Permission Modes

| Mode | Symbolic | Meaning |
|------|----------|---------|
| 777  | rwxrwxrwx | Read, write, execute for all |
| 755  | rwxr-xr-x | Owner full, group & others read/execute |
| 700  | rwx------ | Owner full, no access for others |
| 644  | rw-r--r-- | Owner read/write, group & others read |
| 600  | rw------- | Owner read/write only |

---

## Special Permissions

Setuid (execute as owner):
```
chmod u+s filename
```

Setgid (execute as group):
```
chmod g+s foldername
```

Sticky bit (only owner can delete files in folder):
```
chmod +t foldername
```

---

## Search for Files/Folders by Permission

Find files with exact permission (numeric):
```
find /path -type f -perm 644
```

Find directories with exact permission:
```
find /path -type d -perm 755
```

Find files writable by others:
```
find /path -type f -perm /o+w
```

Find files owned by specific user/group:
```
find /path -user username
find /path -group groupname
```

---

## View Ownership & Permissions Recursively

```
ls -lR /path
```

Check ACL for a folder recursively:
```
getfacl -R /path
```

---

## Useful Tips

- Always check `ls -l` or `stat` before changing permissions  
- Use numeric (`chmod 755`) or symbolic (`chmod u+rwx`) depending on preference  
- Use `sudo` when changing permissions for files you don’t own  
- Sticky bit (`chmod +t`) is important for shared folders like `/tmp`  
- Use `find` to audit or locate files/folders with incorrect permissions  
- Use `less permissions.md` for easy viewing  

---
