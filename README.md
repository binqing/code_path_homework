# Pen Testing Live Targets

Time spent: **X** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:

* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each color is vulnerable to only 2 of the 6 possible exploits. First discover which color has the specific vulnerability, then write a short description of how to exploit it, and finally demonstrate it using screenshots compiled into a GIF.

## Blue

Vulnerability #1: SQL Injection (SQLi)

Description:
* The sites's url: https://35.184.88.145/blue/public/salesperson.php?id=6 is vulnerable to sql injections. The url's id parameter can be modified with sql injection commands, as demonstrated below. 
* The site did not properly sanitize the salesperson.php query.
* Injected the following SQL commands for testing: 
```
    1'OR 1=1' 
```
```
   'or 1=1  
```
```
   'or SLEEP(5)=0--'
```
* The last sql command from above cause the database command to wait for 5 seconds while quering the database.

* Gif Walkthrough: 
                     
<img src="blue-sqli.gif">

Vulnerability #2: Session Hijacking

Description:

* The current session ID of authenticated user can be obtained through a PHP script "public/hacktools/change_session_id.php" provided by codepath and used by an attacker to bypass user login.
* We can use burp to intercept the attacker's login attempt and replace the session ID with the one from an authenticated user.
* Once the intercepted login attempt is forwarded via burp, the attacker's screen is logged in with authenticated user's session ID. 
* The site allows sessions to be a year old, and never regenerates the session ID, even when the user agent string changes. This makes it vulnerable to both session hijacking and session fixation attacks.

* Gif Walkthrough: 

<img src="blue-sessionhijacking.gif">

## Green

Vulnerability #1: Cross-Site Scripting (XSS)

Description:

* A stored XSS vulnerability is found at /green/public/contact.php where anyone can submit feedback on the feedback form. 
* Attacker can inject an XSS in the site's feedback form. 
* Injected XSS command: 
```
    <script>alert('Jasmine found the XSS!');</script>
```
* The XSS script will run and a alert message will be displayed on the screen when an an admin user visits the feedback page.

* Gif Walkthrough:
 
<img src="green-xss.gif">

Vulnerability #2: Username Enumeration

Description:

* The green website is vulnerable to Username Enumeration because site's failure to login error message: "Log in was unsucessfull" is different for valid usernames and invalid usernames. 
* When we try to log in with an invalid username and password, the error message displayed was not bolded.
* However, when we try to log in with a valid username such as " jmonroe99 " and an invalid password, the same error message becomes bolded.  
* This allows us to collect a list of valid usernames and we can use that to perform a brute force password attack on the webiste.  
* Chrome's debugging tool shows that the site assigns two different classes "failed" and "failure" to the failure login error message depending on whether the username name is valid or not. Bolded font is applied to one class but not the other. 

* Gif Walkthrough:

<img src="green-user_enumeration.gif">


## Red

Vulnerability #1: Insecure Direct Object Reference (IDOR)

Description:

<img src="red-idor.gif">


Vulnerability #2: Cross-Site Request Forgery (CSRF)

Description:

<img src="red-csrf.gif">


## Notes

Describe any challenges encountered while doing the work
