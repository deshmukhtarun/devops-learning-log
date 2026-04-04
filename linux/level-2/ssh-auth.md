## Task: Passwordless SSH from Jump Host to App Servers

### Objective
Set up passwordless SSH authentication from user `thor` on the jump host to all three Stratos Datacenter app servers via their respective sudo users.

| App Server | Host     | Sudo User |
|------------|----------|-----------|
| Server 1   | stapp01  | tony      |
| Server 2   | stapp02  | steve     |
| Server 3   | stapp03  | banner    |

---

### Concept
Passwordless SSH uses **asymmetric key pairs**:
- A **private key** stays on the source machine (`~/.ssh/id_rsa`)
- A **public key** is copied to the destination (`~/.ssh/authorized_keys`)

When connecting, SSH proves identity using the private key — no password needed.

---

### Solution

**Step 1 — Check for existing SSH keys on jump host (as thor):**
```bash
ls ~/.ssh/
```

**Step 2 — Generate key pair if none exists:**
```bash
ssh-keygen -t rsa
# Press Enter for all prompts (empty passphrase = truly passwordless)
```

**Step 3 — Copy public key to each app server (one-time password required):**
```bash
ssh-copy-id tony@stapp01
ssh-copy-id steve@stapp02
ssh-copy-id banner@stapp03
```

**Step 4 — Verify passwordless access:**
```bash
ssh tony@stapp01    # should log in with no password
ssh steve@stapp02
ssh banner@stapp03
```

---

### What `ssh-copy-id` does under the hood
Appends `~/.ssh/id_rsa.pub` to `~/.ssh/authorized_keys` on the remote server:
```bash
cat ~/.ssh/id_rsa.pub | ssh tony@stapp01 \
  "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

---

### Key Takeaways
- `ssh-keygen` creates the key pair once; reuse it for all servers
- `ssh-copy-id` is the cleanest way to install a public key remotely
- The sudo user's password is only needed **once** during setup
- After setup, SSH uses key-based auth automatically