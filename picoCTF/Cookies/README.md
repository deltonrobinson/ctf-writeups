# picoCTF: Cookies Writeup

**Author:** Delton Robinson  
**Date:** 7/28/2025  

## Challenge Overview

**Challenge Name:** Cookies  
**Platform:** picoCTF  
**Author of Challenge:** MADSTACKS  
**Flag:** picoCTF{3v3ry1_l0v3s_c00k135_[REDACTED]}

> _"Who doesn't love cookies? Try to figure out the best one."_

Cookies...<br>

---
<!------------------------------------------------------------------------------------------------------------------------------------------------------------------------>
<!--SHORT DESCRIPTION OF CHALLENGE AND INFERENCE REACHED-->
### Initial Observations
<img src="https://i.imgur.com/QYFACED.png" height="80%" width="80%" alt="Initial Description"/><br><br>
Upon launching the site, I saw a basic input field, it requests a type of cookie and responds with how the creator feels about it.<br><br>
<img src="https://i.imgur.com/WtvcAYf.png" height="80%" width="80%" alt="Inputting into Field"/><br>
<img src="https://i.imgur.com/z27oHPq.png" height="80%" width="80%" alt="Site Rendering my Input"/><br>

---
<!------------------------------------------------------------------------------------------------------------------------------------------------------------------------>

## 🧠 Approach
Given the challenge name (`Cookies`), I suspected the vulnerability would be related to the cookies on the website, so I loaded up BurpSuite to analyze the requests in more detail.<br>

<img src="https://i.imgur.com/wcQwVUw.png" height="80%" width="80%" alt="Site Rendering my Input"/><br>

First thing I notice sending the request was ```Cookie```, which had a value of 0. To test if this value changes, I decided to input sugar into the field and observe the Cookie value.<br><br>

<img src="https://i.imgur.com/cd3oDcf.png" height="80%" width="80%" alt="Initial Description"/><br>
As expected, the value did change! The value of Cookie changed from 0 (representing snickerdoodle cookies), to 7 (representing sugar cookies).<br><br>

Having confirmed that the different cookies are tied to the different cookie values in this request, I send the burp request to the Intruder to test many different cookie values and observe the results. I specify the cookie value as the payload, and decide to test values 1 through 20.<br><br>
<img src="https://i.imgur.com/SaQfj0Y.png" height="80%" width="80%" alt="Inputting into Field"/><br>
<img src="https://i.imgur.com/KEZKXMK.png" height="80%" width="80%" alt="Inputting into Field"/><br>
<br><br>
After the Intruder attack finished, I review the results and use the search function to filter for the text "not very special", since I know this text shows up for an incorrect input. Therefore, if a response doesn't contain this string, it must be correct! 
<br><br>
<img src="https://i.imgur.com/3IIsjky.png" height="80%" width="80%" alt="Inputting into Field"/><br>
After moving through the list and just paying attention to the bottom right where it says "1 match", I finally see a payload that received a response containing 0 highlights of the string "not very special". Specifically, the payload that didn't get this response was ```Cookie: name = 18```.<br><br>

Within the Response, I find the flag for this challenge!
