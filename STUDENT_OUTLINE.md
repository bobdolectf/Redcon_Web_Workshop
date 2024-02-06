# Intro

## Getting Started 

Instructor Led Getting Started

## Methodology

Instructor Led discussion on Methodology

## Asset Discovery

Asset discovery is about assessing an organization's attack surface through the lens of application security. A motivated actor will spend days discovering all of your endpoints through a myriad of methods, hence you should be aware of what assets you're leaving out there. A forgotten or misplaced asset can be the foothold an attacker needs to pivot deeper into your network.

Once during an engagement, I discovered an XML External Entities Injection on an endpoint. Surprisingly, the client issued a patch very quickly after disclosing the finding. However, when I went to verify that the patch correctly remedied the vulnerability, I was still able to exploit the endpoint.

The client claimed that all links to the endpoint were removed from their application, so attackers would be unable to locate it and trigger the vulnerability. This is plainly not true, as references to the vulnerable component could still be discovered through forced browsing and web archives. 

The developers failed to fix the vulnerability because they were unaware of how attackers could enumerate their applications. This is an example of why understanding your attack surface is pivotal to maintaining a secure web environment.

Here are a few recon tools and techniques you should be aware of when staging test environments that touch the internet:
* Passive Recon Tools
  * Shodan & Censys constantly crawl the internet and provide a searchable database for attackers to passively surveil your external network.
  * SSL cert registries like crt.sh will record domain names (even internal ones).
  * Wayback Machine & Alienvault provide a glimpse at older versions of applications. They snapshot responses and references, which means an attacker can discover hidden endpoints that are no longer referenced by the main application.
* Active Recon Tools
  * Amass: combines ASN, SSL certificates, historical online databases and DNS records to map your online presence.
  * Massscan/nmap: Quickly performs port scans against a large number of assets. Your applications are not safe on ephemeral ports.
  * Feroxbuster/ffuf: Perform forced browsing and quickly discover unprotected and potentially sensitive directories by using large dictionaries of common web paths.

## Identifying Data Entry Points

Attackers generally want to break a mixture of Confidentiality, Integrity, or Availability (CIA) and thus our approach should focus on answering questions similar to the following:
* Does this data entry point allow us to affect the integrity of the application's data?
* Can we abuse this functionality to cause a denial of service?
* Should this information be available to us? Can we circumvent an access control to access confidential information?

Ultimately the answers to these questions depend on what the organization defines as acceptable. Hence, it is generally a good idea to identify what types of information the organization cares about before assessing application security. For instance, if the organization is a government entity, they may not care if someone can abuse an IDOR bug to retrieve public documents because they are intended to be viewed by everyone. We should narrow our focus on endpoints and bug classes that can impact one of the pillars of the CIA triad in a meaningful way.

Finding these data entry points is typically accomplished by crawling the site with something like [gospider](https://github.com/jaeles-project/gospider) which will recursively follow links of a given URL. The output can be searched for query parameters, web forms, and API endpoints. This data can also be supplimented by web archive queries, which serve to provide a snapshot of an older version of an application.

Even without using a crawler, an attacker can discover potentially sensitive areas to further enumerate. Two common data entry locations are the sitemap.xml and robots.txt files. Most crawlers and scanners will examine the contents of these files, because site administrators usually include paths they do not which to be crawled by polite web crawlers, thus are inherently interesting to an attacker.

Obviously, an attacker's crawler will simply ignore these directives and map all locations included in the robots.txt file. Thus it is recommended to not explicitly call out protected directories. If they are sufficiently protected or simply not referenced in the application, crawlers will not be able to map these locations. Additionally, if you do not wish any polite crawler to map your application, simply use the following configuration:
```
User-agent: *
Disallow: /
```

Lastly, JavaScript files are typically a gold mine for API endpoints and can contain sensitive keys or reveal how administrative functions work without requiring access to restricted administrative content. These files can also trivialize the parameter mining process and lead to access control bypasses. 

## Broken Access Controls 

### Definition 
Access control enforces policy such that users cannot act outside of their intended permissions. Failures typically lead to unauthorized information disclosure, modification, or destruction of all data or performing a business function outside the user's limits.

### Insecure Direct Object Reference
The most common type of Access Control violation is the Insecure Direct Object Reference (IDOR). 

From OWASP's website: "Insecure Direct Object Reference (IDOR) is a vulnerability that arises when attackers can access or modify objects by manipulating identifiers used in a web application's URLs or parameters. It occurs due to missing access control checks, which fail to verify whether a user should be allowed to access specific data."

Example:
Bob browses to https://example.com/profile?userid=1, which returns Bob's account information. If Bob browses to https://example.com/profile?userid=5, the site returns Alice's account information. An attacker can easily iterate through every user's account information by increasing the userid number, which is a very small search space.

In the above case, the application references the userid object directly instead of checking the active user's session prior to disclosing the account information, thus leaking every user's account information. 




### Student Lab 

https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references

### Instructor Solution 


### Real World Example:
I came across a government application that stored users' social security numbers as well as other personally identifiable information. The developers assumed that the users were exclusively interacting with their application through the Graphical User Interface (GUI).

However, by examining the requests sent by the browser to the back-end API, I discovered an account dashboard method within that retrieved the user's account by specified a unique integer user ID value. By guessing a few values above and below my user's ID, I found that the application was not checking the user's access using the session token, but instead relying on the integer.

Using BurpSuite's Intruder, I was able to iterate through 20000 integers in the span of 30 seconds and dump 20000 social security numbers from the application's API. Thankfully, the finding was reported and quickly resolved before the application went live.

### Mitigation
Always perform a check on a user's session before retrieving sensitive information. Even if you utilize a difficult to guess GUID approach (e.g. 6B29FC40-CA47-1067-B31D-00DD010662DA), the session should still be consulted. Complex parameter values can still be leaked in JavaScript or stored in web archives, thus compromising the user's information.

## Business Logic Vulnerabilities 

Most security problems are weaknesses in an application that result from a broken or missing security control (authentication, access control, input validation, etc…). By contrast, business logic vulnerabilities are ways of using the legitimate processing flow of an application in a way that results in a negative consequence to the organization.

For example, in an e-commerce application a POST request to the car may look something like
```
POST /cart-update HTTP/1.1
Host: backend-api.example.com
Content-Type: Application/json

{
"item_id":"13",
"item_price":"14.95",
"item_quantity":"1"
}
```

The application developer assumed that the user would be using the front-end application to interact with the back-end API, and thus made the assumption that all values would be positive when implementing the cart update feature. What would happen if an attacker simply adjusted the price to -99?

If the application possesed a business logic vulnerability based on the assumption that integers would be positive, then the attacker would now be able to purchase the item for $-99. 

Perhaps the system does not allow for a negative cart balance, but the attacker has a $100 item in the cart. They could use the above technique to get a $100 item for $1, thus costing the owning company money.

### Real World Example:
During an engagement with an online banking platform, it was discovered that when someone tried to add an external payment method (like PayPal) to their account, it would send a 4-digit confirmation code to the user's phone before mapping the account to the payment method. However, the application failed to put a rate-limit on the confirmation code submission, so an attacker could simply brute force the 4-digit code in seconds. 

The attacker could now link their bank account to anyone's external payment method by brute-forcing the confirmation code, thus receiving transferred funds intended for the victim's account.

### Mitigation
Never rely solely on client-side validation when performing any sensitive transaction. Always verify data inputs using server-side logic and assume client-side inputs are not to be trusted. 

### Student Lab 
<https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls>

### Instructor solution 


## CTF TIME!!! 

Now for the Challenge! We've set up JuiceShop on your local instance <http://10.6.6.12:3000> 
The scoreboard here: <IP> 
 Go ahead and register and you'll have 20 mins to see who can score the highest with all of your new skillz.
