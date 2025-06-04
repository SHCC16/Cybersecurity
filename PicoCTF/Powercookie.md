# Thought process of solving the Power Cookie Question in PicoCtF

As the question says "PowerCookie" which straightly implies that there would be some kind of cookie modification/handling in the web browser. This is what you see when you launch the instance of the question , 
it redirects you to a webpage which looks like this

![image](https://github.com/user-attachments/assets/6df2ace0-11aa-4484-b193-813fa149e3eb)


When we click on the "continue as guest" pop-up, we are re-directed to a page like this

![image](https://github.com/user-attachments/assets/ea7e3c10-5837-4f52-ab99-cc2ee440936a)

when open the inspect tab and click on the sources tab we see there's no cookie and neither there is anything of use in the network , console etc tab, so we scroll back to the login page again and then open the inspect tab 
and go to the "sources" section , this time we see a guest.js file there below the index php file.

![image](https://github.com/user-attachments/assets/ecf66f2a-8dbe-4f4b-b3b7-a33180e3b853) 

We see that the value is set to be zero to the cookie , Zero which generally defines the "False" value is probably the one obstacle between the user and the flag, I just tried changing the value of 0 to 1 (Which would genrally
mean "True" and let me bypass) and then logged in as the guest.

***Luckily, this didn't require anything else and i was able to obtain the flag.***
