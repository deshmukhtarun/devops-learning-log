# Lab: Updating MOTD for Compliance (Stratos DC)

**Objective:** Standardize the "Message of the Day" (MOTD) across all Nautilus application servers using the approved security template.

---

## 1. Prepare the Template
The approved template is located on the jump host at `/home/thor/nautilus_banner`.

## 2. Implementation Steps
Execute these steps for stapp01, stapp02, and stapp03:

# Step A: Copy the banner from Jump Host to the App Server
# Replace 'user' and 'host' as per your lab credentials (e.g., tony@stapp01)
scp /home/thor/nautilus_banner [user]@[host]:/tmp/

# Step B: Log into the App Server
ssh [user]@[host]

# Step C: Overwrite the MOTD file with the template content
sudo cp /tmp/nautilus_banner /etc/motd

# Step D: Cleanup the temporary file
rm /tmp/nautilus_banner

---

## 3. Verification
To verify the banner is active, simply log out and log back into the server, or run:

cat /etc/motd

**Expected Result:** The content of the file should match the security team's approved template and display immediately upon login.

---