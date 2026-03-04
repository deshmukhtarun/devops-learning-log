# Linux Foundations

## Target Completed

* User creation (various scenarios)
* Group creation and user assignment
* File ownership modification
* Permission management (chmod)
* Access Control List (ACL) configuration
* SSH root login hardening
* File search, copy & backup operations
* String manipulation using sed
* Secure file transfer between servers
* Cron access restriction
* System runlevel / target configuration
* Timezone synchronization
* Firewall rule configuration
* Process limits management
* SELinux installation and configuration

---

# 1. User Management

## Create User with Custom UID and Home

```bash
sudo useradd -u 2101 -d /var/www/aarav -m aarav
```

✔ Custom UID
✔ Custom home directory

---

## Create Non-Interactive User

```bash
sudo useradd -s /sbin/nologin nisha
```

Used for service accounts.

---

## Create User Without Home Directory

```bash
sudo useradd -M rohit
```

---

## Create User with Expiry Date

```bash
sudo useradd -e 2027-12-31 imran
```

Verify:

```bash
sudo chage -l imran
```

---

# 2. Group Management

## Create Group

```bash
sudo groupadd developers_team
```

## Add User to Group

```bash
sudo usermod -aG developers_team aarav
```

Verify:

```bash
getent group developers_team
```

---

# 3. File Ownership & Permissions

## Change Ownership

```bash
sudo chown root:root /opt/app/config.conf
```

## Set Permissions

```bash
sudo chmod 640 /opt/app/config.conf
```

Permission Model:

* Owner → rw-
* Group → r--
* Others → ---

---

# 4. Access Control Lists (ACL)

## Remove Access for Specific User

```bash
sudo setfacl -m u:pooja:0 /opt/app/config.conf
```

## Grant Read-Only Access

```bash
sudo setfacl -m u:vikram:r-- /opt/app/config.conf
```

Verify:

```bash
getfacl /opt/app/config.conf
```

---

# 5. SSH Security Hardening

## Disable Root Login

Edit:

```bash
sudo vi /etc/ssh/sshd_config
```

Set:

```
PermitRootLogin no
```

Restart:

```bash
sudo systemctl restart sshd
```

---

# 6. File Search & Copy Operations

## Find Files Owned by User

```bash
sudo find /data/projects -type f -user aarav
```

## Copy with Directory Structure Preserved

```bash
sudo find /data/projects -type f -user aarav -exec cp --parents {} /backup \;
```

---

# 7. Backup & Transfer

## Create Compressed Archive

```bash
sudo tar -czvf project_backup.tar.gz -C /data projects
```

## Transfer to Storage Server

```bash
scp project_backup.tar.gz user@storage-server:/home/
```

---

# 8. String Manipulation

Replace occurrences of a string inside a file.

```bash
sed -i 's/Random/Marine/g' /root/nautilus.xml
```

---

# 9. Secure File Transfer Between Servers

Copy encrypted file from jump server to app server.

```bash
scp /tmp/nautilus.txt.gpg user@app-server-3:/home/code/
```

---

# 10. Cron Access Restriction

Allow only specific users to manage cron jobs.

Allow user:

```bash
echo "ravi" | sudo tee -a /etc/cron.allow
```

Deny user:

```bash
echo "jerome" | sudo tee -a /etc/cron.deny
```

---

# 11 System Runlevel / Target Configuration

Set system to boot with GUI enabled.

```bash
sudo systemctl set-default graphical.target
```

Verify:

```bash
systemctl get-default
```

---

# 12. Timezone Configuration

Synchronize system timezone.

```bash
sudo timedatectl set-timezone Africa/Bangui
```

Verify:

```bash
timedatectl
```

---

# 13. Firewall Configuration

Allow incoming connections on port 5004/tcp.

```bash
sudo firewall-cmd --set-default-zone=public
sudo firewall-cmd --permanent --zone=public --add-port=5004/tcp
sudo firewall-cmd --reload
```

Verify:

```bash
sudo firewall-cmd --list-ports
```

---

# 14. Process Limits

Limit maximum number of processes for user.

Edit configuration:

```bash
sudo vi /etc/security/limits.conf
```

Add:

```
nfsuser soft nproc 1027
nfsuser hard nproc 2027
```

---

# 15. SELinux Basics

Install required SELinux packages.

```bash
sudo yum install -y selinux-policy selinux-policy-targeted
```

Disable SELinux permanently.

Edit configuration:

```bash
sudo vi /etc/selinux/config
```

Set:

```
SELINUX=disabled
```

Changes take effect after reboot.

---

# 🔎 Key Learnings

* Difference between login and service users
* Importance of `-aG` flag in group management
* Permission number logic (rwx model)
* When to use ACL over standard chmod
* Security benefits of disabling SSH root login
* Preserving directory structure during copy
* Basic backup and transfer workflow
* sed for file manipulation
* Secure file transfer using scp
* Cron access control
* System target configuration
* Timezone synchronization
* Firewall management with firewalld
* Process limit configuration
* Basic SELinux configuration