# PicoCTF — MyGit

**Category:** General Skills  
**Flag:** `picoCTF{1mp3rs0n4t3_g17_345y_02a39618}`

---

## Overview

Push a `flag.txt` file to the remote repository as user `root` with email `root@picoctf`. The server validates the Git commit author before returning the flag.

---

## Solution

### 1. Clone and read the instructions

```bash
git clone ssh://git@foggy-cliff.picoctf.net:62382/git/challenge.git
cd challenge
cat README.md
```

`README.md` states: *"Only flag.txt pushed by `root:root@picoctf` will be updated with the flag."*

### 2. Impersonate the root user

Git author identity is just config — no verification happens by default:

```bash
git config --global user.name "root"
git config --global user.email "root@picoctf"
```

### 3. Commit and push flag.txt

```bash
touch flag.txt
git add flag.txt
git commit -m "flag"
git push origin master
```

### 4. Server response

```
remote: Author matched and flag.txt found in commit...
remote: Congratulations! You have successfully impersonated the root user
remote: Here's your flag: picoCTF{1mp3rs0n4t3_g17_345y_02a39618}
```

---

## Takeaway

Git does **not** verify commit author identity out of the box. Anyone can set `user.name` and `user.email` to any value. This is why GPG/SSH commit signing exists — it cryptographically ties a commit to a verified key, not just a name string.

---

*Author: Muhammad Ihtisyam*
