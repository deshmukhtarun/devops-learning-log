# Lab: Secure Collaborative Directory Setup (Stratos DC)

**Objective:** Create a restricted directory /sysops/data on App Server 3 (stapp03) accessible only by the sysops group with enforced group inheritance.

---

## 1. Directory Creation and Group Ownership
Connect to stapp03 and execute the following:

# Create the directory
sudo mkdir -p /sysops/data

# Change the group ownership to sysops
sudo chgrp sysops /sysops/data

## 2. Permissions and SetGID Bit
The requirement specifies R/W/X for user/group, no access for others, and group ownership for all internal files.

# Set permissions: 
# 2 = SetGID (ensures new files inherit 'sysops' group)
# 7 = rwx for owner
# 7 = rwx for group
# 0 = no access for others
sudo chmod 2770 /sysops/data

---

## 3. Verification
Run these commands to confirm the security settings:

# Check directory permissions and ownership
ls -ld /sysops/data
# Expected: drwxrws--- 2 root sysops ...

# Test Group Inheritance:
# Create a test file and check its group
sudo touch /sysops/data/test_file
ls -l /sysops/data/test_file
# Expected: Group should be 'sysops' even if created by root