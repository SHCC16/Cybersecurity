# SHOP

## CATEGORY- REVERSE ENGINEERING

### CHALLENGE DESCRIPTION -
Best Stuff - Cheap Stuff, Buy Buy Buy... Store Instance: source. 
The shop is open for business at
```bash
nc mercury.picoctf.net 24851
```

### HINT-
1. Always check edge cases when programming

### SOLUTION

When we run the program, we see it's a menu driven program which looks like this



![image](https://github.com/user-attachments/assets/5bccac70-6ba2-4975-ac83-d510efb168a1)

Looking at the items it's easy to figure out that the only thing which looks "fruitful" and promising is the "Fruitful Flag" , another indication in focusing towards this item is how we have 40 coins
and only the flag is the item which we can't buy because of its price according to the menu, hence I understood that the main part in solving the question boils down to obtaining the "Fruitful Flag".

Even though it's mathematically not possible to buy the flag from 40 coins, I still tried to obtain and as expected it showed me an error as shown below-



![image](https://github.com/user-attachments/assets/1c957b70-50a0-4d58-b80d-973674df1a11)

I dabbled with all the options present from trying to first buy  and sell stuff during which I noticed that the program showed that I have -10 coins after selling which doesn't make sense because practically I 
shouldn't have been able to complete the transaction, that's when the hint again struck me which said "Always check edge cases" which made me understood that there's some issue with the way they are calculating
the number of coins a user has after each transaction. There seemed to be an integer overflow where the program was not checking if the number was negative or positive. Hence to counter this i tried to purchase 
an item in negative quantity and it worked




![image](https://github.com/user-attachments/assets/8420f6ab-548b-480a-bb84-17b16613986f)



After obtaining the flag i first thought that it's some kind of weird cipher text but later it made sense that these are just the ASCII codes while i was going through the various kinds of cipher texts, hence 
I used an online ASCII converter and the result was :-

```bash
picoCTF{b4d_brogrammer_532bcd98}
```


Hence solved xd

