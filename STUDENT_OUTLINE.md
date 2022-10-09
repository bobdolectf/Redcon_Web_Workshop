# Intro

## Getting Started 

Quick intro, make sure all students have access to the Kali station and are fully functional.  Give an overview of what we are going to workshop, why we chose the topics (OWASP and personal fav's).

## Methodology
Talk about broad methodology, this is not meant to get you pulling bounties from H1 or Synack but more to have cognizance of common web app mistakes

## Discussion Broken Access Controls 
Access control enforces policy such that users cannot act outside of their intended permissions. Failures typically lead to unauthorized information disclosure, modification, or destruction of all data or performing a business function outside the user's limits

### Student Lab (5 mins)
https://portswigger.net/web-security/access-control/lab-url-based-access-control-can-be-circumvented

### Instructor Solution 
https://portswigger.net/web-security/access-control/lab-url-based-access-control-can-be-circumvented

## Discussion Business Logic Vulnerabilities 
Most security problems are weaknesses in an application that result from a broken or missing security control (authentication, access control, input validation, etc…). By contrast, business logic vulnerabilities are ways of using the legitimate processing flow of an application in a way that results in a negative consequence to the organization.

### Student Lab 
https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls

### Instructor solution 
https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls

## Discussion Injection
An application is vulnerable to attack when:

- User-supplied data is not validated, filtered, or sanitized by the application.

- Dynamic queries or non-parameterized calls without context-aware escaping are used directly in the interpreter.

- Hostile data is used within object-relational mapping (ORM) search parameters to extract additional, sensitive records.

- Hostile data is directly used or concatenated. The SQL or command contains the structure and malicious data in dynamic queries, commands, or stored procedures.

### Demo 
https://portswigger.net/web-security/os-command-injection/lab-simple

### Student Lab
https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays
https://portswigger.net/web-security/os-command-injection/lab-blind-output-redirection

### Instructor Solution 
https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays


## Discussion Server Side Request Forgery 
SSRF flaws occur whenever a web application is fetching a remote resource without validating the user-supplied URL. It allows an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall, VPN, or another type of network access control list (ACL).

### Demo 
https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost

### Student Lab
https://portswigger.net/web-security/ssrf/lab-ssrf-with-blacklist-filter

### Instructor Solution 
https://portswigger.net/web-security/ssrf/lab-ssrf-with-blacklist-filter


## Discussion File Upload 
Uploaded files represent a significant risk to applications. The first step in many attacks is to get some code to the system to be attacked. Then the attack only needs to find a way to get the code executed. Using a file upload helps the attacker accomplish the first step.

The consequences of unrestricted file upload can vary, including complete system takeover, an overloaded file system or database, forwarding attacks to back-end systems, client-side attacks, or simple defacement. It depends on what the application does with the uploaded file and especially where it is stored.

### Demo 
 https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-obfuscated-file-extension

### Student Lab 
https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-path-traversal

### Instructor Solution 
 https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-path-traversal

## Discussion Authentication 
Confirmation of the user's identity, authentication, and session management is critical to protect against authentication-related attacks. There may be authentication weaknesses if the application:

- Permits automated attacks such as credential stuffing, where the attacker has a list of valid usernames and passwords.

- Permits brute force or other automated attacks.

- Permits default, weak, or well-known passwords, such as "Password1" or "admin/admin".

- Uses weak or ineffective credential recovery and forgot-password processes, such as "knowledge-based answers," which cannot be made safe.

- Uses plain text, encrypted, or weakly hashed passwords data stores (see A02:2021-Cryptographic Failures).

- Has missing or ineffective multi-factor authentication.

- Exposes session identifier in the URL.

- Reuse session identifier after successful login.

- Does not correctly invalidate Session IDs. User sessions or authentication tokens (mainly single sign-on (SSO) tokens) aren't properly invalidated during logout or a period of inactivity.

### Demo 
https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses

https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-simple-bypass

### Student Lab 
https://portswigger.net/web-security/authentication/password-based/lab-broken-brute-force-protection-multiple-credentials-per-request


## CTF TIME!!! 
Now for the Challenge! We've set up JuiceShop on your local instance and a CTFd scoreboard here: <IP>  Go ahead and register and you'll have 20 mins to see who can score the highest with all of your new skillz.
