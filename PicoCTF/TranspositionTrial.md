# Transposition Trial

# CATEGORY- CRYPTOGRAPHY

# Challenge Description
Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around!
The first word seems to be three letters long, maybe you can use that to recover the rest of the message. Download the corrupted message here.

Since the challenge mentioned that the first letter is three letters long and the corrupted text said-

***heT"fl "g a"s i"icp"CTo"{7F"4NR"P05"1N5"_16"_35"P3X"51N"3_V"091"B0A"E}2"***

It was easy to enough to figure out that the first world was "The" and the rest of the words before the bracket meant "The flag is picoCTF" , the only trick in the question was to include the spaces as a character 
in the 3 words and shifting the 3 words to the right for example "heT" changes to "The"

so dividing the corrupted message into 3 characters i got-
![image](https://github.com/user-attachments/assets/34e58d26-8243-46ad-9619-24329e8818df)

and arranging every 3 character in the same format we get

![image](https://github.com/user-attachments/assets/9b282dd1-8955-443d-a9ca-b01e35e8e8cf)


Challenge solved xd:)
