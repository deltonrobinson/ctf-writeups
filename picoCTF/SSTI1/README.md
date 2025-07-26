# picoCTF: SSTI1 Writeup

**Author:** Delton Robinson  
**Date:** 7/22/2025  

## Challenge Overview

**Challenge Name:** SSTI1  
**Platform:** picoCTF  
**Author of Challenge:** VENAX  
> _"I made a website where you can announce anything you want!"_

That’s the hint we’re given — a simple webpage that echoes back whatever input you type in an `<h1>` tag. Sounds harmless, right?<br>

---
<!------------------------------------------------------------------------------------------------------------------------------------------------------------------------>
<!--SHORT DESCRIPTION OF CHALLENGE AND INFERENCE REACHED-->
### Initial Observations
<img src="https://i.imgur.com/NyJIidn.png" height="80%" width="80%" alt="Initial Description"/><br><br>
Upon launching the site, I saw a basic input field, which renders whatever I type into it in h1 format.<br><br>
<img src="https://i.imgur.com/QifthOU.png" height="80%" width="80%" alt="Inputting into Field"/><br>
<img src="https://i.imgur.com/brdSiOE.png" height="80%" width="80%" alt="Site Rendering my Input"/><br>

---
<!------------------------------------------------------------------------------------------------------------------------------------------------------------------------>

## 🧠 Approach
Given the challenge name (`SSTI1`), I suspected the vulnerability would be **Server-Side Template Injection** (SSTI). To test this, I used the classic SSTI test payload:
```
{{3*3}}
```
The output was 9, indicating that the site is indeed vulnerable to **Server-Side Template Injection** (SSTI) attacks.<br><br>

<img src="https://i.imgur.com/WSBOe1E.png" height="80%" width="80%" alt="Initial Description"/><br>
<img src="https://i.imgur.com/5A9lEKA.png" height="80%" width="80%" alt="Initial Description"/><br>

Having confirmed the vulnerability of the website to SSTI attakcs, I research more payloads that I can use to exfiltrate data from the vulnerability.
<br><br>
During my search, I came upon a github repo (https://github.com/payloadbox/ssti-payloads) detailing multiple payloads to exploit SSTI within vulnerable sites. 
<br><br>

<img src="https://i.imgur.com/xYLCYT8.png" height="80%" width="80%" alt="Initial Description"/><br>

After searching the repo, I found the payload I needed to execute commands and navigate the directory. 
```
{{config.__class__.__init__.__globals__['os'].popen('ls').read()}}
```
Injecting this payload allows me to run the command ```ls```, which lets me view all of the files within the current directory.

<img src="https://i.imgur.com/J996iYn.png" height="80%" width="80%" alt="Initial Description"/><br>
<img src="https://i.imgur.com/9Pp2mFy.png" height="80%" width="80%" alt="Initial Description"/><br>

Viewing the files within the directory, I can clearly see a ```flag``` file, so I proceed to inject the same payload but change the command from ```ls``` to ```cat flag```, which provides me the flag I need to complete the challenge!

<img src="https://i.imgur.com/FgMUtuq.png" height="80%" width="80%" alt="Initial Description"/><br>
