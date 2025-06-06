# VAULT DOOR TRAINING 

## CATEGORY - REVERSE ENGINEERING

### CHALLENGE DESCRIPTION
Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors.
Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the
vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what
the password is for that vault door. As a warmup, we have created a replica vault in our training facility. The source code for the training vault is here: (the link is in the website)

### HINTS 
The password is revealed in the program's source code.

### ***SOLUTION***
When we look at the hint , it is very easy to makeout that for the password , we just have to carefully look in the source-code provided in the question. The source code is a java
program which when open into our code editor looks something like this

![image](https://github.com/user-attachments/assets/1c0b0646-0e4c-4019-9ed5-6ac89861361e)


From here it was very easy to makeout that the flag is (if you know basic java syntax)
```bash
picoCTF{w4rm1ng_Up_w1tH_jAv4_be8d9806f18}
```

Hence Solved xd
