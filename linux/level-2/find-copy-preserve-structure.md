## Task: Find and Copy Files with Directory Structure Preserved

### Objective
On App Server 3, find all `.css` files under `/var/www/html/official` and copy
them (with parent directory structure intact) to `/official` — without copying
the entire source directory.

---

### Key Commands

| Tool | Purpose |
|------|---------|
| `find -type f` | match files only, excludes directories |
| `find -name "*.css"` | filter by extension |
| `cp --parents` | preserves full path when copying |
| `-exec ... \;` | runs a command per found file |

---

### Solution

**Step 1 — SSH into App Server 3:**
```bash
ssh banner@stapp03
```

**Step 2 — Preview matching files:**
```bash
find /var/www/html/official -type f -name "*.css"
```

**Step 3 — Copy with parent structure:**
```bash
sudo find /var/www/html/official -type f -name "*.css" -exec cp --parents {} /official \;
```

**Step 4 — Verify:**
```bash
ls -lR /official
```

Output should mirror the source tree under `/official/var/www/html/official/...`

---

### Key Takeaways
- `-type f` is essential — skips directories, symlinks, etc.
- `cp --parents` is the cleanest way to preserve directory structure
- `-exec cp --parents {} /official \;` runs once per file (`\;`) vs `+` which batches — both work here but `\;` is safer with `--parents`
- The destination `/official` must exist beforehand (`sudo mkdir -p /official`)