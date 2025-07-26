# picoCTF: Guess My Cheese Part 1 Writeup

**Author:** Delton Robinson  
**Date:** 7/23/2025  

## Challenge Overview

**Challenge Name:** Guess My Cheese (Part 1)  
**Platform:** picoCTF  
**Author of Challenge:** ADITIN  
**Flag:** picoCTF{ChEeSy******}  

> _"Try to decrypt the secret cheese password to prove you're not the imposter!"_

Seems like we need to decrypt a "secret cheese password" in order to get the flag.<br>

---
<!------------------------------------------------------------------------------------------------------------------------------------------------------------------------>
<!--SHORT DESCRIPTION OF CHALLENGE AND INFERENCE REACHED-->
### Initial Observations
<img src="https://i.imgur.com/YenmscJ.png" height="80%" width="80%" alt="Initial Description"/><br><br>

This challenge doesn't seem to be liked much by others, so lets netcat into the server and see what within this program has everyone against this specific challenge!

---
<!------------------------------------------------------------------------------------------------------------------------------------------------------------------------>

## 🧠 Approach

After connecting to the server, I'm greeted with a short story about a rat who lost his best friend Squeexy. It's our job to guess the secret cheese (whatever it may be), and "prove" that we are in fact Squeexy.<br><br>
However, the prompt states that the cheeses are top secret and limited edition, implying that the secret cheese changes respective to each instance of the program. <br><br>
I start by attempting to guess ```cheddar```, which is incorrect. It was a bit too on the nose to be the correct answer, and I used up one of my 3 tries, so I reconnect to the server to try again from the beginning.<br><br>

<img src="https://i.imgur.com/bTZ60ax.png" height="100%" width="100%" alt="Initial Description"/><br><br>

This time, I start by attempting to encrypt ```cheddar```, and I get the string ```KFIJJMV``` as output. This leads be to believe that I am dealing with a substitution cipher, since both d's in ```cheddar``` became j's. <br><br>
Also, since we know the encoded secret cheese is ```GYQVEIKIE```, we now know for certain that the secret cheese contains two e's, since the encoded ```cheddar``` turned the e into an i. <br><br>

I navigate to ```https://www.dcode.fr/affine-cipher``` in order to test my belief that this is a substitution cipher, and I input the encoded ```cheddar``` string ```KFIJJMV```.<br><br>
<img src="https://i.imgur.com/yt9rOTp.png" height="100%" width="100%" alt="Initial Description"/><br><br>
The second result decoded the text back into '''cheddar''', as well as listing out the A & B coefficients of the cipher, being 
```
A = 25 | B = 12
```

With the A & B coefficients, I can attempt to decode the mysterious secret cheese! I update my manual parameters within affine decoder, and proceed to input the previously mentioned encoded secret cheese, ```GYQVEIKIE```<br><br>
<img src="https://i.imgur.com/YZrVoxN.png" height="100%" width="100%" alt="Initial Description"/><br><br>
When decoded with the coefficients ```A = 25 | B = 12```, the secret cheese ```GYQVEIKIE``` decodes into ```GOWRIECEI```, and with a potential secret cheese, I return the webshell to attempt to prove that we are in fact Squeexy<br><br>

<img src="https://i.imgur.com/Zm2eKd9.png" height="100%" width="100%" alt="Initial Description"/><br><br>

Now, I’ve never heard of a cheese called “GOWRIECEI” before, but I’m also not a rat; they may know something I don’t.<br><br>

<img src="https://i.imgur.com/h9GY2TU.png" height="100%" width="100%" alt="Initial Description"/><br><br>

And it seems like they do! GOWRIECEI was authenticated as the correct secret cheese, and I was given the flag I desired!
