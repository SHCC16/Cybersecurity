# heap 0

## CATEGORY- BINARY EXPLOITATION

### Challenge Description

Are overflows just a stack concern?
Download the binary here.
Download the source here.
Connect with the challenge instance here:
nc tethys.picoctf.net 57242

### Hints

What part of the heap do you have control over and how far is it from the safe_var? 

### SOLUTION

Connected to the challenge using the given `nc` command and it runs a program which looks something like this 

```bash

Welcome to heap0!
I put my data on the heap so it should be safe from any tampering.
Since my data isn't on the stack I'll even let you write whatever info you want to the heap, I already took care of using malloc for you.

Heap State:
+-------------+----------------+
[*] Address   ->   Heap Data
+-------------+----------------+
[*]   0x5772672b32b0  ->   pico
+-------------+----------------+
[*]   0x5772672b32d0  ->   bico
+-------------+----------------+

1. Print Heap:          (print the current state of the heap)
2. Write to buffer:     (write to your own personal block of data on the heap)
3. Print safe_var:      (I'll even let you look at my variable on the heap, I'm confident it can't be modified)
4. Print Flag:          (Try to print the flag, good luck)
5. Exit

Enter your choice:
```
Now as a sane person would do in his/her first attempt , I tried the "Print Flag" option but it said 
```bash
Looks like everything is still secure
```
as expected , I dabbled with the other options as well and couldn't find anything meaningful out of it and then i remembered there was a source code as well (xd)
as I  traversed through the source code (Which was written in c) i found everything pretty normal in the first two go's until I saw how was the program working to give me the flag
which looked something like this:-

![image](https://github.com/user-attachments/assets/325436cf-d5a4-4eac-b5ab-901f0e3baa4f)

Looking at this its easy to make out that we will get the flag if the input is not "bico" and hence I understood that I just need to work around this and do something to make that flag printed.
Upon inspecting the code more I noticed the addresses of pico and bico but still I wasn't able to make anything fruitful out of it. After scratching my brain for 15 more minutes I pondered upon
the name of the question and the description which said "Heap" which is to understand in easier terms a continuous stream of memory and reading the description again , I understood that I need to overflow
the heap memory, I searched about the addresses and it suggested me to subtract them which resulted into 32 bytes (yeah i took a little help)


So I just needed to overflow the input and trick the code (which was by giving a 33 byte input) , I did the following and was able to obtain the flag.


![image](https://github.com/user-attachments/assets/8087094c-784a-46f3-a5ad-f7b5ad5c1d17)


Hence solved xd
