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


# RSA
## About
RSA is named after its creators.
[insert creators]
It was invented to solve the problem of key sharing and is one of the older asymmetric crypto systems.
Keys are made up of a very large number, 1024 bit is a small key, you can get up to 3072 bit keys, which is the product of 2 primes, and two other numbers discussed later. 
The very large number is needed for encryption and decryption, so it's in both the public and private keys, whereas the 2 related numbers are divided with one public and one private.

## How it works
RSA is based on a couple of principles:
* It is hard to factor large numbers
* Euler's Theorem that if $gcd(M,n) = 1$ then $M^{\phi(n)} \equiv 1 (\text{mod } n)$
  * Note that $\phi$ is the totient function

Also note that if that sounds complicated, this math is about to be more complicated.

### Key Generation
To generate a key, you will first generate 2 large prime numbers, which we will call $p$ and $q$.
Their product, $p \cdot q$ will be called $n$. $n$'s only factors are $p$ and $q$ since they were prime.

Next, calculate $\phi(n)$. Because of how the totient function works, we can calculate it by multiplying the totient of $n$'s factors, $p$ and $q$, so 
$\phi(n) = \phi(p) \cdot \phi(q)$ and since $p$ and $q$ are prime, their totients are just 1 less than themselves, giving us $\phi(n) = (p-1)(q-1)
* Note here: This means that $\phi(n)$ is easy for us to calculate since we know $n$'s factors. Without $p$ and $q$ the totient is basically impossible to calculate.

Next, we just pick any value $e$ as long as $gcd(e, \phi(n)) = 1$, which will ensure that $e$ is invertable mod $\phi(n)$, which is important because
the next we calculate $d = e^{-1} \text{ mod } \phi(n)$, or in other words the value $d$ such that $d \cdot e \equiv 1 \text{ mod } \phi(n)$.
* Note that calculating the inverse is actually very easy. As long as you have $e$ and $\phi(n)$, you're all set. That's why $\phi(n)$ needs to be a protected secret.

As long as all of these properties have been satisfied, congrats! Your public key is now $(n, e)$ and your private key is $(n, d)$. 

### Encryption and decryption
That's great, but how the heck does any of that let us encrypt anything??

Encryption is deceptively simple. For these examples $x$ is the message and $y$ is the encrypted message. To encrypt:
$y = x^e \text{ mod } n$

To decrypt: $x = y^d \text{ mod } n$

Easy right? But how the heck does any of that work?

The encryption just converts your message into a different number, so let's focus on what happens during decryption. 

What we do is $y^d \text{ mod } n$. Since we know $y = x^e \text{ mod } n$, we can plug it in to get $(x^e)^d \text{ mod }n$

This is equivalent to $x^{ed} \text{ mod }n$

Since we know $ed \equiv 1 \text{ mod } \phi(n)$, that means that $ed = k \cdot \phi(n) + 1$ for some unknown value $k$. It won't matter what it is, so let's plug it in to get: 
$x^{k\phi(n)+1} \text{ mod } n$

Another algebra rewrite gives us: $(x^{\phi(n)})^k \cdot x \text{ mod } n$

Using Euler's theorem, we know $x^{\phi(n)} \text{ mod } n \equiv 1$, so we can rewrite to $(1)^k \cdot x \text{ mod }n$

Which of course is just $x \text{ mod }n$, giving us back our original message.

## Possible attacks
### Factor n
The brute force style attack on RSA is to factor $n$. If you can do that, you can calculate $\phi(n)$ and get $d$ from $e$. 
It's a common challenge in CTF's to factor an $n$ and you typically don't need to brute force it. 
There are calculators online that have already calculated the factors for $n$s that are too small.





