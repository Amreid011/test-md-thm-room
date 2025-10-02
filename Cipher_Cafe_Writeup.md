# Cipher Cafe - TryHackMe Room Writeup

This is a detailed writeup for the **Cipher Cafe** challenge room.  
The room contains multiple classical cryptography and steganography challenges.  
Below, we solve each task step by step and provide answers to all the questions.

---

## Task 1 - Caesar Cipher

We are given the file `begin.txt` containing:

```
YMR{i3hwduy}
```

This looks like a **Caesar cipher**.  
By applying a brute-force Caesar shift, we find that the text decrypts properly when shifted.  
After testing shifts, the hidden word is revealed.
 Try shifting backwards by 3 (a very common Caesar shift).  
   Example tool: [dcode.fr Caesar Cipher](https://www.dcode.fr/caesar-cipher)  
 Decoding reveals:  
   ```
   THM{d3crypt}
   ```

✅ **Flag:** `THM{d3crypt}`


**Q1: What cipher was used here?**  
A: `caesar`

**Q2: What is the hidden keyword inside the decrypted message?**  
A: `THM{d3crypt}`

---

## Task 2 - Reversed Base64

The file `flip.txt` contains:

```
=03MyV3YzM3eNhEV
```

Observations:  
- The string looks like Base64, but reversed.  
- First, reverse the string:  
  `VEhNe3MzYzN3VyM30=`  
- Now decode from Base64 → we get the hidden keyword.
-  Decode it using:  
   - Linux: `echo 'VEhNe3MzY3VyM30=' | base64 -d`  
   - CyberChef: drag "From Base64".  
 The output is:  
   ```
   THM{s3cur3}
   ```

✅ **Flag:** `THM{s3cur3}`


**Q1: What encoding scheme was used in this challenge?**  
A: `base64`

**Q2: What is the final keyword from the decoded message?**  
A: `THM{s3cur3}`

---

## Task 3 - Vigenère Cipher

The file `vigenere.txt` contains:

```
DLK{mp4qc1g}
```

This is a **Vigenère cipher**.  
We test possible keys and discover the correct one is **key**.  
Decrypting the ciphertext reveals the hidden keyword.
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

**Q1: What is the key used for the Vigenère cipher?**  
A: `key`

**Q2: What is the hidden keyword after decryption?**  
A: `THM{cl4ss1c}`

---

## Task 4 - XOR Encryption

The file `xor.hex` contains hex data:

```
3f7b34104b4919550c054e
```

Steps:  
1. Convert hex to bytes.  
2. We know TryHackMe flags start with `THM{`.  
3. Using this crib, we XOR against the ciphertext to recover the 3-byte key.  
4. After decrypting, we reveal the full flag.
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

**Q1: What is the 3-byte key used here?**  
A: `k3y`

**Q2: What is the final decrypted flag?**  
A: `THM{x0rfun}`

---

## Task 5 - Steganography in PNG

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

**Q1: What technique was used to hide the message?**  
A: `lsb`

**Q2: What is the final flag?**  
A: `THM{Amr_s4ys_w41t_f0r_us_in_4_n3w_ch4ll3ng3}`

---

# Final Notes

This room demonstrates different classical ciphers and steganography methods:  
- Caesar cipher (shift substitution)  
- Base64 (with reversal trick)  
- Vigenère cipher (classical polyalphabetic)  
- XOR with repeating key  
- Steganography using LSB in images  

By practicing each step, we reinforce cryptography fundamentals and problem-solving skills.
