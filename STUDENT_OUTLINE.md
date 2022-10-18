# Intro

## Getting Started 

Instructor Led Getting Started

## Methodology

Instructor Led discussion on Methodology

## Broken Access Controls 

Access control enforces policy such that users cannot act outside of their intended permissions. Failures typically lead to unauthorized information disclosure, modification, or destruction of all data or performing a business function outside the user's limits

### Student Lab (5 mins)

<https://portswigger.net/web-security/access-control/lab-url-based-access-control-can-be-circumvented>

### Instructor Solution 

## Business Logic Vulnerabilities 

Most security problems are weaknesses in an application that result from a broken or missing security control (authentication, access control, input validation, etc…). By contrast, business logic vulnerabilities are ways of using the legitimate processing flow of an application in a way that results in a negative consequence to the organization.

### Student Lab 
<https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls>

### Instructor solution 

## Command Injection

An application is vulnerable to attack when:

- User-supplied data is not validated, filtered, or sanitized by the application.

- Dynamic queries or non-parameterized calls without context-aware escaping are used directly in the interpreter.

- Hostile data is used within object-relational mapping (ORM) search parameters to extract additional, sensitive records.

- Hostile data is directly used or concatenated. The SQL or command contains the structure and malicious data in dynamic queries, commands, or stored procedures.

### Student Lab

<https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays>

<https://portswigger.net/web-security/os-command-injection/lab-blind-output-redirection>

### Instructor Solution 


## Server Side Request Forgery 

SSRF flaws occur whenever a web application is fetching a remote resource without validating the user-supplied URL. It allows an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall, VPN, or another type of network access control list (ACL).

### Student Lab
<https://portswigger.net/web-security/ssrf/lab-ssrf-with-blacklist-filter>

### Instructor Solution 

## File Upload 
Uploaded files represent a significant risk to applications. The first step in many attacks is to get some code to the system to be attacked. Then the attack only needs to find a way to get the code executed. Using a file upload helps the attacker accomplish the first step.

The consequences of unrestricted file upload can vary, including complete system takeover, an overloaded file system or database, forwarding attacks to back-end systems, client-side attacks, or simple defacement. It depends on what the application does with the uploaded file and especially where it is stored.

### Student Lab 
<https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-path-traversal>

### Instructor Solution 

## HTTP Request Smuggling (10 Mins)
 
HTTP request smuggling is a technique for interfering with the    way a web site processes sequences of HTTP requests that are      received from one or more users. Request smuggling                vulnerabilities are often critical in nature, allowing an         attacker to bypass security controls, gain unauthorized access    to sensitive data, and directly compromise other application      users.

Most HTTP request smuggling vulnerabilities arise because the HTTP specification provides two different ways to specify where a request ends: the Content-Length header and the Transfer-Encoding header.

The Content-Length header is straightforward: it specifies the length of the message body in bytes.

The Transfer-Encoding header can be used to specify that the message body uses chunked encoding. This means that the message body contains one or more chunks of data. Each chunk consists of the chunk size in bytes (expressed in hexadecimal), followed by a newline, followed by the chunk contents. The message is terminated with a chunk of size zero.

### Student Lab 
https://portswigger.net/web-security/request-smuggling/lab-obfuscating-te-header

### Instructor Solution 

## CTF TIME!!! 
Now for the Challenge! We've set up JuiceShop on your local instance and a CTFd scoreboard here: <IP>  Go ahead and register and you'll have 20 mins to see who can score the highest with all of your new skillz.
