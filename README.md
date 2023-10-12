# Weak-RSA
My solution to HTB Weak-RSA without using RsaCtfTool, since I have to find one yet. We going to do this the simple and OLD fashioned way. Solution file is called **more.py** 

## Solution 
Look its very simple here. You dont need a fancy tool to solve this problem. This challenge is named *weak* for a reason. We're given a public key and from there we can extract juicy info from the key by using the following command 
```
openssl rsa -text -pubin -in public_key.key 
```
This command will give us the exponent (e) and modulus (n). <br><br>
Also check out my cool RSA slides here: https://docs.google.com/presentation/d/1UDapUyetU0RhW9nxci2SU6a93h8uCu7ErAAymIlpBeQ/edit?usp=sharing <br>
ANYWAYS. Once we do whatever to convert the e and n to its decimal representation, we can now try to see if we can factorize that big assssss number. My fav website [factordb.com] (http://factordb.com/)
