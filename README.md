# Weak RSA
My solution to HTB Weak RSA without using RsaCtfTool. We going to do this the simple and OLD fashioned way. I actually had to look really hard to find a solution that didn't use RsaCtfTool, and it was actually impossible. So here's the best way to solve this problem. I promise you'll feel super fulfilled. Solution file is called **more.py** 

## Solution 
Look its very simple here. You dont need a fancy tool to solve this problem. This challenge is named *weak* for a reason. We're given a public key and from there we can extract juicy info from the key by using the following command 
```
openssl rsa -text -pubin -in public_key.key 
```
This command will give us the exponent (e) and modulus (n). <br>

Also check out my cool RSA slides here: https://docs.google.com/presentation/d/1UDapUyetU0RhW9nxci2SU6a93h8uCu7ErAAymIlpBeQ/edit?usp=sharing <br>

ANYWAYS. Once we do whatever to convert the e and n to its decimal representation, we can now try to see if we can factorize that big assssss number (which you can ^^). My fav website factordb.com. From there we'll find the respective p and q values and thats **ALL YOU NEED** to break RSA! 

Now we take the enc file we have, its in binary no problem. Use openssl to erncode it to base64, so it makes it easier to work with:
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

Cryptodome offers a very useful tool called inverse, and I would highly recommend everyone uses that tool to dervie d. 

Once we get d, we just perform the decryption formula, like so: 
```
decimalval = pow(ct,d,n)
```
Then we can use another cryptodome function to take the decimal value and convert it to binary text:
```
long_to_bytes(decimalval)
```
AND BOOM. 
<img width="77" alt="Screenshot 2023-10-12 at 1 27 06 AM" src="https://github.com/katstews/Weak-RSA/assets/112781868/4d4efcd1-8e4d-44f0-b832-65f7a9ddab07">
<br>
I would also like to thank Cryptohack, yall really prepped me for this.
