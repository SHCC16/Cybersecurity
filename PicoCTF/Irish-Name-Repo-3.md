# Irish-Name-Repo-3

## CATEGORY- WEB EXPLOITATION

### CHALLENGE DESCRIPTION- 
There is a secure website running at https://jupiter.challenges.picoctf.org/problem/40742/ (link) or http://jupiter.challenges.picoctf.org:40742. Try to see if you can login as admin!

### Hints-
1. Seems like the password is encrypted.

### Solution
When we launch the website we see a random webpage with some irishmen , on exploring the webpage we notice that the next page buttons are not working and when we explore more we find the "Admin login"



![image](https://github.com/user-attachments/assets/514c4bfb-81f0-4d74-a46a-a5039afa2014)


The admin login redirects us to a login page like this- 


![image](https://github.com/user-attachments/assets/3e6aa90f-2059-445f-9cba-3f734acca4a3)

I intercepted the login request the same way as in "Intro to Burp" and on doing so we notice that the login request is sent using POST to the page with a "debug" value of 0, on editing the debug value to 1 and sending the request again (I thought i'll get the flag here) we see that that the password i have entered is jumbled to something different altogether , as i try again, it happens the same way, to check if its randomly changing the password everytime or there is some set pattern , I entered the same password again and i could make out that there was a shift of exactly 13 letters everytime.

Hence i used a simple SQL injection query which didn't include alphabets and I got the flag

Hence solved xd
