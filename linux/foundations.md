# Linux Foundations

## Target Completed

- User creation (various scenarios)
- Group creation and user assignment
- File ownership modification
- Permission management (chmod)
- Access Control List (ACL) configuration
- SSH root login hardening
- File search, copy & backup operations

---

# 1 User Management

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

# 2 Group Management

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

# 3 File Ownership & Permissions

## Change Ownership

```bash
sudo chown root:root /opt/app/config.conf
```

## Set Permissions

```bash
sudo chmod 640 /opt/app/config.conf
```

Permission Model:

- Owner → rw-
- Group → r--
- Others → ---

---

# 4 Access Control Lists (ACL)

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

# 5 SSH Security Hardening

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

# 6 File Search & Copy Operations

## Find Files Owned by User

```bash
sudo find /data/projects -type f -user aarav
```

## Copy with Directory Structure Preserved

```bash
sudo find /data/projects -type f -user aarav -exec cp --parents {} /backup \;
```

---

# 7 Backup & Transfer

## Create Compressed Archive

```bash
sudo tar -czvf project_backup.tar.gz -C /data projects
```

## Transfer to Storage Server

```bash
scp project_backup.tar.gz user@storage-server:/home/
```

---

# 🔎 Key Learnings

- Difference between login and service users
- Importance of `-aG` flag in group management
- Permission number logic (rwx model)
- When to use ACL over standard chmod
- Security benefits of disabling SSH root login
- Preserving directory structure during copy
- Basic backup and transfer workflow
