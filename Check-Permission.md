
# Linux Find Commands To Check Permissions

# 📌 Find Files and Directories with Specific Permissions

### 🔹 Find files with 777 permissions (read, write, execute for all users)
```bash
find / -perm 777 -type f 2>/dev/null
```
### 🔹 Find directories with 777 permissions
```bash
find / -perm 777 -type d 2>/dev/null
```
### 🔹 Find directories with the **sticky bit** (1777)
```bash
find / -perm 1777 -type d 2>/dev/null
```
### 🔹 Find world-writable files (others have write permission)
```bash
find / -type f -perm -o=w 2>/dev/null
```
```
find / -type f -perm -o+w 2>/dev/null
```
### 🔹 Find files where **others** have full 777 permissions
```bash
find / -type f -perm -o=wrx 2>/dev/null
```
### 🔹 Find writable directories for **others**
```bash
find / -type d -perm -o=w 2>/dev/null
```
### 🔹 Find writable directories owned by the **current user**
```bash
find / -writable -type d 2>/dev/null
```
### 🔹 Find readable directories for the **current user**
```bash
find / -readable -type d 2>/dev/null
```

# 🔐 Find SUID/SGID Files

### 🔹 Find **SUID** (Set User ID) files
```bash
find / -type f -perm -u=s 2>/dev/null
```
```
find / -perm -4000 2>/dev/null  # Alternative method
```
### 🔹 Find **SGID** (Set Group ID) files
```bash
find / -type f -perm -g=s 2>/dev/null
```
```
find / -perm -2000 2>/dev/null  # Alternative method
```
### 🔹 Find **SGID** directories
```bash
find / -type d -perm -g=s 2>/dev/null
```
### 🔹 Find both **SUID and SGID** files
```bash
find / -perm -6000 2>/dev/null
```

# 👤 Find Files Based on Ownership

### 🔹 Find files owned by a **specific user** (e.g., `root`) with SUID
```bash
find / -user root -perm -4000 2>/dev/null
```
### 🔹 Find files **not owned** by any user
```bash
find / -nouser 2>/dev/null
```

# 📁 Find Specific File Types

### 🔹 Find writable **configuration files**
```bash
find / -name "*.conf" -type f -writable 2>/dev/null
```
### 🔹 Find **cron jobs** with writable permissions
```bash
find /etc/cron* /var/spool/cron* -type f -writable 2>/dev/null
```
### 🔹 Find **potentially sensitive files** (backup, private keys, SSH keys)
```bash
find / -type f \( -name "*.bak" -o -name "*.old" -o -name "*.backup" -o -name "id_rsa*" -o -name "authorized_keys" \) 2>/dev/null
```
### 🔹 Find files that might contain **exposed credentials**
```bash
find / -type f \( -name "*.log" -o -name "*.txt" -o -name "*.ini" \) -exec grep -i 'password' {} + 2>/dev/null
```
### 🔹 Find **backup files** (compressed archives)
```bash
find / -type f \( -iname "*.zip" -o -iname "*.tar" -o -iname "*.7z" -o -iname "*.rar" -o -iname "*.bz2" -o -iname "*.gz" -o -iname "*.tbz" -o -iname "*.tgz" \) > backupfiles.txt
```

##⚡ Find Files with Special Capabilities

### 🔹 Find files with **special Linux capabilities**
```bash
getcap -r / 2>/dev/null
```

# Bonus: Additional Useful `find` Commands

### 🔹 Find files modified **in the last 24 hours**
```bash
find / -type f -mtime -1 2>/dev/null
```
### 🔹 Find files modified **more than 7 days ago**
```bash
find / -type f -mtime +7 2>/dev/null
```
### 🔹 Find files **larger than 100MB**
```bash
find / -type f -size +100M 2>/dev/null
```
### 🔹 Find **empty** files and directories
```bash
find / -type f -empty 2>/dev/null  # Empty files
```
```
find / -type d -empty 2>/dev/null  # Empty directories
```
### 🔹 Find and **delete** files with `.tmp` extension
```bash
find / -type f -name "*.tmp" -delete 2>/dev/null
```
### 🔹 Find files **modified in the last 10 minutes**
```bash
find / -type f -mmin -10 2>/dev/null
```
### 🔹 Find and **execute a command** on matching files
```bash
find / -type f -name "*.log" -exec rm {} \; 2>/dev/null  # Delete all .log files
```
```
find / -type f -name "*.log" -exec chmod 644 {} \; 2>/dev/null  # Change permissions
```
