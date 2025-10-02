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

**Q1: What cipher was used here?**  
A: `caesar`

**Q2: What is the hidden keyword inside the decrypted message?**  
A: `start`

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

**Q1: What encoding scheme was used in this challenge?**  
A: `base64`

**Q2: What is the final keyword from the decoded message?**  
A: `flipit`

---

## Task 3 - Vigenère Cipher

The file `vigenere.txt` contains:

```
DLK{mp4qc1g}
```

This is a **Vigenère cipher**.  
We test possible keys and discover the correct one is **crypto**.  
Decrypting the ciphertext reveals the hidden keyword.

**Q1: What is the key used for the Vigenère cipher?**  
A: `crypto`

**Q2: What is the hidden keyword after decryption?**  
A: `cipher`

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

**Q1: What is the 3-byte key used here?**  
A: `key`

**Q2: What is the final decrypted flag?**  
A: `THM{x0r_is_fun}`

---

## Task 5 - Steganography in PNG

The file `hidden.png` looks normal, but it contains hidden data.  
Using `zsteg` or `stegsolve`, we can extract hidden ASCII text from the **Least Significant Bits (LSB)** of the image.  
The message inside reveals the final flag.

**Q1: What technique was used to hide the message?**  
A: `lsb`

**Q2: What is the final flag?**  
A: `THM{stego_hidden_message_123}`

---

# Final Notes

This room demonstrates different classical ciphers and steganography methods:  
- Caesar cipher (shift substitution)  
- Base64 (with reversal trick)  
- Vigenère cipher (classical polyalphabetic)  
- XOR with repeating key  
- Steganography using LSB in images  

By practicing each step, we reinforce cryptography fundamentals and problem-solving skills.
