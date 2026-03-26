# Lab: Cron Job Configuration on Nautilus App Servers

**Objective:** Install the cronie package and schedule a root-level cron job on all Nautilus app servers in the Stratos DC.

---

## 1. Installation and Service Setup
Execute these commands on stapp01, stapp02, and stapp03:

sudo yum install -y cronie
sudo systemctl start crond
sudo systemctl enable crond

## 2. Cron Job Implementation
Requirement: Run echo hello > /tmp/cron_text every 5 minutes for the root user.

# Add the job to root's crontab using a one-liner:
echo "*/5 * * * * echo hello > /tmp/cron_text" | sudo crontab -u root -

---

## 3. Verification
| Action | Command | Expected Result |
| :--- | :--- | :--- |
| Check Service | sudo systemctl status crond | active (running) |
| Verify Crontab | sudo crontab -l -u root | */5 * * * * echo hello > /tmp/cron_text |
| Check Output | cat /tmp/cron_text | File exists (after 5 mins) |

---