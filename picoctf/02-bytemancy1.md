# PicoCTF — Bytemancy-1

**Category:** General Skills  
**Flag:** `picoCTF{h0w_m4ny_e's???_6e0cc4c6}`

---

## Overview

Connect via netcat. The server asks you to send a specific ASCII decimal character repeated a specific number of times, side-by-side with no spaces.

---

## Solution

### 1. Connect and read the prompt

```bash
nc foggy-cliff.picoctf.net 49531
```

Server responds:

```
Send me ASCII DECIMAL 101 1751 times, side-by-side, no space.
```

### 2. Identify the character

ASCII decimal `101` = `e`

### 3. Generate and send the string

```bash
python3 -c "print('e' * 1751)" | nc foggy-cliff.picoctf.net 49531
```

Or if already inside the nc session, paste the output of:

```bash
python3 -c "print('e' * 1751)"
```

### 4. Server response

```
picoCTF{h0w_m4ny_e's???_6e0cc4c6}
```

---

## Takeaway

Know your ASCII table. For challenges like this, scripting the response with a one-liner is always faster and less error-prone than doing it manually.

---

*Author: Muhammad Ihtisyam*
