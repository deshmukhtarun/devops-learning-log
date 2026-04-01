# Lab: Text Alteration and Filtering on Nautilus App Server 3

**Objective:** Use command-line tools to filter lines and replace specific whole words within the /home/BSD.txt file in the Stratos DC environment.

---

## 1. Task A: Delete Lines Containing a Specific Word
**Requirement:** Remove all lines containing the word "code" (case-sensitive) and save the output to /home/BSD_DELETE.txt.

# Using grep -v to select lines that do NOT match the pattern "code"
grep -v "code" /home/BSD.txt > /home/BSD_DELETE.txt

## 2. Task B: Replace Specific Whole Words
**Requirement:** Replace every occurrence of the word "or" with "them" and save to /home/BSD_REPLACE.txt.
**Constraint:** Ensure words like "organize" or "contributor" are not altered.

# Using sed with word boundaries (\b) to target only the standalone word "or"
sed 's/\bor\b/them/g' /home/BSD.txt > /home/BSD_REPLACE.txt

---

## 3. Verification
To confirm the operations were successful, run the following checks:

| Action | Command | Expected Result |
| :--- | :--- | :--- |
| Check Deletion | grep "code" /home/BSD_DELETE.txt | No output (lines are gone) |
| Check Replacement | grep -w "or" /home/BSD_REPLACE.txt | No output (all "or" are "them") |
| Check Integrity | grep "organize" /home/BSD_REPLACE.txt | Word remains "organize" |