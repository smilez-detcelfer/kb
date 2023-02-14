portswigger.net - 
seclists - lists for wuzzing and bruteforce
payloadallthethings - cheet sheet resource
hacktrix.xyz - cheet sheet resource

![[Pasted image 20230204073043.png]]
![[Pasted image 20230204073126.png]]
![[Pasted image 20230204073252.png]]
![[Pasted image 20230204073339.png]]


http headers:
content-type - sending data type
boudary - delimiter

*crawling (spidering)* scrript goes to every link
*dirbasting* - find files and directories by dictionary (dirsearch, dirbuster)
*searching virtual servers* smth.domain.com (burp intruder with dns dictionary)
*searching .git/.svn files* (searching source code for analysis)
*user enumeration*
*api enumeration* (find missing functional level access contorl in api)
-   *brute path and methods*
    -   [https://github.com/assetnote/kiterunner](https://github.com/assetnote/kiterunner)
-   *javascript path and methods finder*
    -   [https://github.com/GerbenJavado/LinkFinder](https://github.com/GerbenJavado/LinkFinder)
*sql injection*:
* bypass
* union-based
* error-based
* boolean-blind
* time-based
* stacked queries
sql injection finder - sqlmap
*SSTI (server side template injection)'n*
*Race Condition* - on DB level (for update, for share)
*XXS wft*
*CSRF Cross-Site Request Forgery* (redirect )'
SOP (same origin policy)
browser defence mechanism, which blocks access to  http responce from site with other SOP
![[Pasted image 20230204165955.png]]
![[Pasted image 20230204170100.png]]


### sql injection defence
validation
safety calls to sql:
* **sanitisation** (concatination)
* **prepared statements**
![[Pasted image 20230204091343.png]]

* **ORM (Object-relational mapping)** prepared statements inside
![[Pasted image 20230204092223.png]]
know how your ORM creates mapping
know how hackers used known vulnerabilities
create whiti lists for table

Session:
data stored on server side.
Server give id to user browser to identify him

authentification:
* random session id (stores in cookie)
* JWT (json web tokens) https://jwt.io ( can see but can't change it)
if session signature correct - cookies accepted
if we try to modify session data  - server won't accepted such cookies
* JWM (json web messaging) *encrypted session data* (user even can't read it)
hacker can try to bruteforce it (offline bruteforce)
![[Pasted image 20230204112329.png]]


## access contorl
* **functional level contro**l (control on role model)
problem - *missing functional level access contorl*
* **object level control**
problem - *insecure direct object reference (IDOR)* 

![[Pasted image 20230204122335.png]]

## SSTI server side template injection
https://portswigger.net/web-security/server-side-template-injection
flask ssti:
{{7 * 7}}

## Race condition
when you make few queries to database, and new values still is not updated

Python serialisation
ssrf
xml extended entity
prf rendering