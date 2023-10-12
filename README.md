# Weak RSA
My solution to HTB Weak RSA without using RsaCtfTool, since I have to find one yet. We going to do this the simple and OLD fashioned way. Solution file is called **more.py** 

## Solution 
Look its very simple here. You dont need a fancy tool to solve this problem. This challenge is named *weak* for a reason. We're given a public key and from there we can extract juicy info from the key by using the following command 
```
openssl rsa -text -pubin -in public_key.key 
```
This command will give us the exponent (e) and modulus (n). <br>

Also check out my cool RSA slides here: https://docs.google.com/presentation/d/1UDapUyetU0RhW9nxci2SU6a93h8uCu7ErAAymIlpBeQ/edit?usp=sharing <br>

ANYWAYS. Once we do whatever to convert the e and n to its decimal representation, we can now try to see if we can factorize that big assssss number. My fav website factordb.com. From there we'll find the respective p and q values and thats **ALL YOU NEED** to break RSA! 

Now we take the enc file we have, its in binary no problem. Use openssl to encrypt it to base64:
```
openssl base64 -in flag.enc -out flag.64
```

Ok. Now read the darn file and convert the following base64 values to its repspective decimal values, and now we can start performing simple RSA. 

**Decryption formula**:
```
plaintext = ciphertext**(d) % n
```
**Decryption Key formula (d)**:
```
d = inverse(e,phi)
```
**phi**:
```
phi = (p-1) * (q-1)
```
Now we see why p and q is important. You need to know p and q to derive phi, which you use phi to dervie the decryption key d.

Basically you take your ciphertext (in its decminal rep) and take it to the power of your decryption key THEN modulo it by n (the modulus value). 
