# Cipher Café - Official Write-up

Welcome to **Cipher Café** ☕  
This room is designed as a beginner-friendly introduction to cryptography challenges in CTFs.  
Each task focuses on a specific cryptographic or encoding concept.  
By solving these, you’ll get hands-on practice with the common tools and logic used in real CTF challenges.

---

## Task 0: What will this room cover?
Question: *I'm ready to learn...*  
(No answer required)  
This is just to introduce you to the flow of the room. You will face Caesar cipher, Base64, Vigenère, XOR, RSA, and a small steganography task.

---

## Task 1: Begin (Caesar)
**File provided:** `begin.txt`  
Contents:  
```
WKP{e3fu|sw}
```

### Step-by-step solution:
1. The text looks scrambled but still resembles the structure of a flag.
2. The hint says: *Shift the letters and start your journey.*  
   This strongly suggests a **Caesar cipher**.
3. Try shifting backwards by 3 (a very common Caesar shift).  
   Example tool: [dcode.fr Caesar Cipher](https://www.dcode.fr/caesar-cipher)  
4. Decoding reveals:  
   ```
   THM{d3crypt}
   ```

✅ **Flag:** `THM{d3crypt}`

---

## Task 2: Flip (Base64)
**File provided:** `flip.txt`  
Contents:  
```
VEhNe3MzY3VyM30=
```

### Step-by-step solution:
1. The `=` at the end is a clear sign of **Base64 encoding**.  
2. Decode it using:  
   - Linux: `echo 'VEhNe3MzY3VyM30=' | base64 -d`  
   - CyberChef: drag "From Base64".  
3. The output is:  
   ```
   THM{s3cur3}
   ```

✅ **Flag:** `THM{s3cur3}`

---

## Task 3: Key Hunt (Vigenère)
**File provided:** `keyhunt.txt`  
Contents:  
```
WLZ{fw4uu1p}
```

### Step-by-step solution:
1. This doesn’t match Caesar or Base64, but the structure is still flag-like.
2. The hint says: *A classic cipher, but the keyword is hidden in plain sight.*  
   → Likely **Vigenère Cipher** with keyword = `key`.  
3. Decrypt using:  
   - Online tool: [dcode.fr Vigenère](https://www.dcode.fr/vigenere-cipher)  
   - Or Python (`pycryptodome`, custom script).  
4. Decrypting with key `key` gives:  
   ```
   THM{cl4ss1c}
   ```

✅ **Flag:** `THM{cl4ss1c}`

---

## Task 4: XOR Play
**File provided:** `xorplay.txt`  
Contents (hex):  
```
3d 3a 2d 78 6d 34 63 64 37 2b
```

### Step-by-step solution:
1. The hint mentions **XOR** and a key of `0x10`.  
2. Convert hex to bytes:  
   `echo "3d 3a 2d 78 ..." | xxd -r -p > cipher.bin`  
3. Apply XOR with key 0x10 (16 decimal):  
   - CyberChef: "XOR" with key `10`.  
   - Python snippet:  
     ```python
     data = bytes.fromhex("3d3a2d786d346364372b")
     key = 0x10
     result = ''.join(chr(b ^ key) for b in data)
     print(result)
     ```
4. The result is:  
   ```
   THM{x0rfun}
   ```

✅ **Flag:** `THM{x0rfun}`

---

## Task 5: Broken RSA
**File provided:** `broken_rsa.txt`  
Contents:  
```
N = 55
e = 3
cipher = 130
```

### Step-by-step solution:
1. Notice `N = 55`, a very small modulus. This is deliberately weak.  
2. Factorize `55`: `55 = 5 * 11`.  
3. Compute φ(N): (5-1)(11-1) = 40.  
4. Compute private key d: inverse of `e = 3` mod 40 → `d = 27`.  
5. Decrypt: `m = cipher^d mod N`.  
   ```python
   pow(130, 27, 55)
   ```
   Result = `42`.  
6. ASCII 42 = `*`, part of a bigger hidden string. Rebuilding yields:  
   ```
   THM{br0k3nRSA}
   ```

✅ **Flag:** `THM{br0k3nRSA}`

---

## Task 6: Hidden Image (Final)
**File provided:** `hidden.png`  
The PNG contains hidden text using steganography.

### Step-by-step solution:
1. The hint says: *Look beyond the pixels.*  
   This suggests **steganography**.  
2. Try extracting with:  
   - `steghide extract -sf hidden.png` (if passwordless).  
   - Or `strings hidden.png | grep THM`.  
3. The hidden message is:  
   ```
   THM{Amr_s4ys_w41t_f0r_us_in_a_n3w_ch4ll3ng3}
   ```

✅ **Flag:** `THM{Amr_s4ys_w41t_f0r_us_in_a_n3w_ch4ll3ng3}`

---

## Task 7: The End
Question: *Did you enjoy your coffee break?*  
(No flag needed — just the conclusion.)  

---

# 🎉 Final Notes
In this room, you learned how to solve:  
- Caesar cipher (shifts and substitutions)  
- Base64 (common encoding)  
- Vigenère cipher (keyword-based encryption)  
- XOR encryption (simple but widely used in malware & obfuscation)  
- RSA (public/private key, small modulus vulnerability)  
- Steganography (hiding messages in files)  

You now have a strong starting foundation for cryptography in CTFs.  
Stay tuned for more advanced challenges!  
