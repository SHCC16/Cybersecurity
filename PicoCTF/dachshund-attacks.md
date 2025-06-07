# DACHSHUND-ATTACKS

## CATEGORY- CRYPTOGRAPHY

### CHALLENGE DESCRIPTION- 
What if d is too small? Connect with `nc mercury.picoctf.net 41508.`

### Hint-
What do you think about my pet? dachshund.jpg


### Solution - 
On connecting to the challenge using the `nc` command we get the following screen


![image](https://github.com/user-attachments/assets/6b6e66c1-0b8d-4fa3-ac0e-b8ee8969a487)


and its easy to make out that it is a RSA challenge, which means its encrypted using RSA , by connecting it with the name of the challenge I get to something called "Weiner's RSA" we see that it's a method to 
attack RSA when the d is too small (but no use for another half an hour) , I found that there's a python pre-built script called "Weiner Attack" .

I installed the implementation in the shell
