# Weak-RSA
My solution to HTB Weak-RSA without using RsaCtfTool, since I have to find one yet. We going to do this the simple and OLD fashioned way. Solution file is called **more.py** 

## Solution 
Look its very simple here. You dont need a fancy tool to solve this problem. This challenge is named *weak* for a reason. We're given a public key and from there we can extract juicy info from the key by using the following command 
> openssl rsa -text -pubin -in public_key.key 

This command will give us the exponent (e) and modulus (n) 
