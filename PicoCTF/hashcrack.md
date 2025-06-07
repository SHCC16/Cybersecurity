# Hashcrack

## CATEGORY - CRYPTOGRAPHY

### CHALLENGE DESCRIPTION-
A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server?
Access the server using `nc verbal-sleep.picoctf.net 57819`

### HINTS-

1)Understanding hashes is very crucial. Read more here.
2)Can you identify the hash algorithm? Look carefully at the length and structure of each hash identified.
3)Tried using any hash cracking tools?

### Solution
After connecting to the challenge using the `nc` command we see a program like this in the output


![image](https://github.com/user-attachments/assets/52ac32da-c175-45f3-96cb-c3d89835ec5c)

I used a hash identifier as it was mentioned in the hints and i got the first one as MD5 then I used an online decrypter and it gave the output "password123" entering which I got another hash
and using the same procedure as above, I got the type as SHA1 and on decrypting it we got "letmein" and after that we get another random hash which upon inspecting is of the type "SHA256" and when we decrypt that has
we get "qwerty098" , which on entering gives us the flag. Xd 

![image](https://github.com/user-attachments/assets/48814584-081b-4f8d-b54c-ae2cbb2d9436)


Hence solved xd
