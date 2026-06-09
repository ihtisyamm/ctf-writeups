# PicoCTF — Printer Shares

**Category:** General Skills  
**Difficulty:** Easy  
**Points:** 50  
**Flag:** `picoCTF{...}` *(retrieved from flag.txt)*

---

## Overview

A file was accidentally sent to a network printer's SMB share. Connect to the print server and retrieve it.

---

## Solution

### 1. Identify the share

List available shares on the target using `smbclient`:

```bash
smbclient -L //mysterious-sea.picoctf.net -p 60422 -N
```

Output:
```
Sharename       Type      Comment
---------       ----      -------
shares          Disk      Public Share With Guests
IPC$            IPC       IPC Service (Samba 4.19.5-Ubuntu)
```

The `shares` share is open to guests — no credentials needed (`-N` flag).

### 2. Connect and list files

```bash
smbclient //mysterious-sea.picoctf.net/shares -p 60422 -N
```

Inside the SMB shell:

```
smb: \> ls
  dummy.txt
  flag.txt
```

### 3. Download the flag

```bash
smb: \> mget flag.txt
```

Then read it locally:

```bash
cat flag.txt
```

---

## Key Commands

| Command | Purpose |
|---------|---------|
| `smbclient -L //<host> -p <port> -N` | List shares anonymously |
| `smbclient //<host>/<share> -p <port> -N` | Connect to a share anonymously |
| `ls` | List files in the share |
| `mget <file>` | Download a file |

---

## Takeaway

SMB shares misconfigured with guest/anonymous access are a common finding in real engagements. Always enumerate with `-N` (no password) first before assuming auth is required. Tools like `smbmap` can also automate share enumeration across a network.

---

*Author: Muhammad Ihtisyam*
