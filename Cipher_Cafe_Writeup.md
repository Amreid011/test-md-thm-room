# Cipher Café - Official Write-up

Welcome to **Cipher Café**! ☕ This challenge room is designed to introduce beginners to the basics of cryptography through six fun and simple tasks. Each task involves a different classic cipher or encoding method. Let’s go through them one by one.

---

## Task 1: Begin (Caesar)
**File given:** `begin.txt`  
The file contains:  
```
WKP{e3fu|sw}
```

**Hint:** "Shift the letters and start your journey."

This is a **Caesar Cipher** with a shift of `-3`. Decoding it gives:  
```
THM{d3crypt}
```

✅ **Flag:** `THM{d3crypt}`

---

## Task 2: Flip (Base64)
**File given:** `flip.txt`  
The file contains:  
```
VEhNe3MzY3VyM30=
```

**Hint:** "Sometimes you just need to flip the base."

This is **Base64 encoding**. Decoding gives:  
```
THM{s3cur3}
```

✅ **Flag:** `THM{s3cur3}`

---

## Task 3: Key Hunt (Vigenère)
**File given:** `keyhunt.txt`  
The file contains:  
```
WLZ{fw4uu1p}
```

**Hint:** "A classic cipher, but the keyword is hidden in plain sight."  
Keyword = `key`

Decrypting with **Vigenère cipher** using key `key`:  
```
THM{cl4ss1c}
```

✅ **Flag:** `THM{cl4ss1c}`

---

## Task 4: XOR Play
**File given:** `xorplay.txt`  
The file contains raw hex:  
```
3d 3a 2d 78 6d 34 63 64 37 2b
```

**Hint:** "Bitwise operations can hide secrets. Key = 0x10."

Apply XOR with key `0x10`:  
```
THM{x0rfun}
```

✅ **Flag:** `THM{x0rfun}`

---

## Task 5: Broken RSA
**File given:** `broken_rsa.txt`  
The file contains:  
```
N = 55
e = 3
cipher = 130
```

**Hint:** "Small keys break easily."

RSA modulus `N = 55` → factors: `5 * 11`.  
φ(N) = (5-1)(11-1) = 40  
d = inverse of e mod φ(N) = 27  
Decrypt: `130^27 mod 55 = 42` → ASCII(42) = `*` → part of message.  
Final reconstructed message:  
```
THM{br0k3nRSA}
```

✅ **Flag:** `THM{br0k3nRSA}`

---

## Task 6: Hidden Image (Final)
**File given:** `hidden.png`  
The image has hidden data using steganography.

**Hint:** "Look beyond the pixels."

Using `steghide extract` or `strings` reveals the hidden text:  
```
THM{Amr_s4ys_w41t_f0r_us_in_a_n3w_ch4ll3ng3}
```

✅ **Flag:** `THM{Amr_s4ys_w41t_f0r_us_in_a_n3w_ch4ll3ng3}`

---

# 🎉 Congratulations!
You’ve completed Cipher Café and explored:  
- Caesar Cipher  
- Base64 Encoding  
- Vigenère Cipher  
- XOR Cipher  
- RSA Basics  
- Steganography  

This room introduces the foundation of cryptography that will help you in bigger challenges.  

