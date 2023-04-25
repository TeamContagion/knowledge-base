# Crypto Systems
Let's talk about some crypto systems! These are popular and common crypto systems.
Here we will explain how it works, what makes it secure, and possible attacks.

# AES
## About
AES stands for the Advanced Encryption Standard.
It is the evolution of DES, discussed later.
It is a symmetric system, so the same key is used to encrypt and decrypt.
It is secure (probably) and efficient in both hardware and software, so it is very common as part of larger encryption schemes,
for example using an assymetric scheme to exchange AES keys.
Key sizes are typically 128, 192, or 256 bits.

## How it Works
Let's get into the math of it.
[Insert math here]

## Possible Attacks

### Brute Force
The most basic attack on any crypto system is brute forcing the key. 
This requires that you check every single possible key.
In AES, and any good crypto algorithm, you can't tell when a candidate key is closer to the real key, so you just have to test every single one and see if it gives you something real.
In CTFs there is no way they will ask you to brute force an AES key. Possibly you may have to brute force a password and the hash is the key, but even that is rare 
(password brute forcing challenges are somewhat common, but they aren't crypto challenges).

### ECB Oracle Attack
If the encryption is running in ECB mode, you can append information to the flag before encryption, and it tells you the encrypted output, you can perform this attack.
A great write up for it can be found here: https://zachgrace.com/posts/attacking-ecb/.
To summarize, if a block is 8 bytes, you can append 7 known bytes to the beginning to make the first block encrypted your 7 characters plus the first character of the flag.
Record the output.
Next, append those same 7 characters plus a character to test.
If the first block of this new output is the same as the old output, that means the first letter of the flag is that character you tested.
In this way, you can brute force all possible characters. 
For a CTF I recommend brute forcing from a list of characters that are reasonable for a flag, for example letters, numbers, and symbols, but not unprintable characters.
Next, append 6 characters and the known first character. 
This means the first block is your 6 characters followed by the first and second characters of the flag.
To brute force, use those 6 characters, the first character of the flag, and the character you want to test. 

