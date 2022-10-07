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
https://portswigger.net/web-security/os-command-injection/lab-blind-output-redirection

## Discussion Directory Traversal (10 Mins)

### Demo (1 Mins)
https://portswigger.net/web-security/file-path-traversal/lab-simple

### Student Lab (5 mins)
https://portswigger.net/web-security/file-path-traversal/lab-absolute-path-bypass

### Instructor Solution (2 Mins)
https://portswigger.net/web-security/file-path-traversal/lab-absolute-path-bypass

## Discussion Authentication (10 Mins)

### Demo
https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses
https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-simple-bypass

### Student Lab
https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-broken-logic

## CTF TIME!!!

