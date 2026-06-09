# PicoCTF — Text Transformations

**Category:** General Skills  
**Flag:** `picoCTF{Reverse1ng_t3xt_Tr4ns0rm@t10ns_3n939318}`

---

## Overview

Connect via netcat. The server shows a transformed flag and hints at what transformation was applied. Enter the correct Linux command to reverse each step until the original flag is recovered.

---

## Solution

Connect:

```bash
nc <host> <port>
```

### Step-by-step reversals

| Step | Transformation applied | Reverse command |
|------|----------------------|-----------------|
| 1 | Base64 encoded | `base64 -d` |
| 2 | String reversed | `rev` |
| 3 | Underscores replaced with dashes | `tr '-' '_'` |
| 4 | Curly braces replaced with parentheses | `tr '()' '{}'` |
| 5 | ROT13 applied to letters | `tr 'A-Za-z' 'N-ZA-Mn-za-m'` |

---

## Gotchas

- **No pipes or echo allowed.** The server only accepts bare commands. `echo "..." | tr` will be rejected.
- **Step 3 direction.** The hint says `tr '_' '-'` but the flag at that point already has dashes — you need to swap them back to underscores, so the correct command is `tr '-' '_'`.
- **ROT13 is self-inverse.** Applying it once both encodes and decodes.

---

## Takeaway

Read the hint, but always look at the actual current state of the flag to confirm which direction the reversal needs to go. Hint wording can be misleading on operand order for `tr`.

---

*Author: Muhammad Ihtisyam*
