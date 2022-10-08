# Intro

## Getting Started 

Quick intro, make sure all students have access to the Kali station and are fully functional.  Give an overview of what we are going to workshop, why we chose the topics (OWASP and personal fav's).

## Methodology
Talk about broad methodology, this is not meant to get you pulling bounties from H1 or Synack but more to have cognizance of common web app mistakes

## Discussion Broken Access Controls (10 Mins)

### Demo (2 Mins)
https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality

//walkthrough
Enumerate site, nothing really on the main page.  Check out robots.txt and see that the admin panel is listed and navigate to it

https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality-with-unpredictable-url

//walkthrough
notice this in the source /admin-al12ax and navigate to it

### Student Lab (5 mins)
https://portswigger.net/web-security/access-control/lab-url-based-access-control-can-be-circumvented

### Instructor Solution (1 Mins)
https://portswigger.net/web-security/access-control/lab-url-based-access-control-can-be-circumvented


//walkthrough
add X-Original-URL: /admin to request and see the difference
GET /?username=carlos HTTP/1.1
X-Original-URL: /admin/delete

## Discussion Business Logic Vulnerabilities (10 Mins)

### Demo (2 Mins)

https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-high-level

//walkthrough
log in with weiner : peter and add the jacket to your cart, check the http history and give it a look, if you go negative with it you can get a negative balance and then you can balance out the transaction 

### Student Lab (5 Mins)
https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls

### Instructor solution (2 Mins)
https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls

// walkthrough
Add to cart, then modify the price parameter
productId=1&redir=PRODUCT&quantity=1&price=1

## Discussion Injection (10 Mins)

### Demo 
https://portswigger.net/web-security/os-command-injection/lab-simple

//walkthrough

modify the storeId parameter  productId=1&storeId=1;whoami

### Student Lab
https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays
https://portswigger.net/web-security/os-command-injection/lab-blind-output-redirection

### Instructor Solution (2 Mins)
https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays
//walkthrough
Modify the email parameter, note that this is blind so you are really just counting to see if you are getting execution
csrf=0pmJEQphMpXzJH6DZ24qLkxUgeWCZ95g&name=asdf&email=asdffsd%40gmail.com||ping+-c+10+127.0.0.1||&subject=asfd&message=asfd

https://portswigger.net/web-security/os-command-injection/lab-blind-output-redirection
//walkthrough
open any item and check the image location then add your output to it
https://0a8e003a03edd6b0c07c39a800c800f4.web-security-academy.net/image?filename=output.txt
csrf=tUtP0VJ2JE9m9JyBb5ck8TnPI7oWxiri&name=asfd&email=x%40gmail.com||whoami>/var/www/images/output.txt||&subject=afd&message=safd


## Discussion Directory Traversal (10 Mins)

### Demo (1 Mins)
https://portswigger.net/web-security/file-path-traversal/lab-simple
//walkthrough
navigate around and find an image request and modify
GET /image?filename=../../../../../etc/passwd

### Student Lab (5 mins)
https://portswigger.net/web-security/file-path-traversal/lab-absolute-path-bypass

### Instructor Solution (2 Mins)
https://portswigger.net/web-security/file-path-traversal/lab-absolute-path-bypass
//walkthrough
navigate around and find an image request and modify
GET /image?filename=/etc/passwd HTTP/1.1

## Discussion Authentication (10 Mins)

### Demo (2 mins)
https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses
//walkthrough
make sure you only copy the bottom third of the usernames, throw those into intruder and brute the username should be "autodiscover"
grab the middle third of the passwords and spray that at password, it should be "555555"

https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-simple-bypass
//walkthrough
log in to your account, check out the page after 2FA.   /my-account

log out and log in as carlos and instead of the pin put that in

### Student Lab (5 mins)
https://portswigger.net/web-security/authentication/password-based/lab-broken-brute-force-protection-multiple-credentials-per-request

for the passwords break out a little vimfu :%s/$/"/g and :%s/^/"/g
take the passwords and make sure you pass them in an array on an intercept
"username":"carlos",
"password": [
"12345",
]

## CTF TIME!!! 

