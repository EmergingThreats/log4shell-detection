# Attack String Detection


## Protocol detection strings

These signatures are designed to detect the attack strings for the various JNDI supported network services:

| Inbound SID | Outbound SID | msg                                                                       |
|-------------|--------------|---------------------------------------------------------------------------|
| 2034647     |              | ET EXPLOIT Apache log4j RCE Attempt (http ldap) (CVE-2021-44228)          |
| 2034649     | 2034759      | ET EXPLOIT Apache log4j RCE Attempt (tcp ldap) (CVE-2021-44228)           |
| 2034651     | 2034761      | ET EXPLOIT Apache log4j RCE Attempt (udp ldap) (CVE-2021-44228)           |
| 2034656     | 2034766      | ET EXPLOIT Apache log4j RCE Attempt (udp ldaps) (CVE-2021-44228)          |
| 2034657     | 2034767      | ET EXPLOIT Apache log4j RCE Attempt (tcp ldaps) (CVE-2021-44228)          |
| 2034658     | 2034768      | ET EXPLOIT Apache log4j RCE Attempt (http ldaps) (CVE-2021-44228)         |
| 2034648     | 2034758      | ET EXPLOIT Apache log4j RCE Attempt (http rmi) (CVE-2021-44228)           |
| 2034650     | 2034760      | ET EXPLOIT Apache log4j RCE Attempt (tcp rmi) (CVE-2021-44228)            |
| 2034652     | 2034762      | ET EXPLOIT Apache log4j RCE Attempt (udp rmi) (CVE-2021-44228)            |
| 2034653     | 2034763      | ET EXPLOIT Apache log4j RCE Attempt (udp dns) (CVE-2021-44228)            |
| 2034654     | 2034764      | ET EXPLOIT Apache log4j RCE Attempt (tcp dns) (CVE-2021-44228)            |
| 2034655     | 2034765      | ET EXPLOIT Apache log4j RCE Attempt (http dns) (CVE-2021-44228)           |
| 2034667     | 2034788      | ET EXPLOIT Apache log4j RCE Attempt (udp iiop) (CVE-2021-44228)           |
| 2034668     | 2034787      | ET EXPLOIT Apache log4j RCE Attempt (tcp iiop) (CVE-2021-44228)           |
| 2034714     | 2034790      | ET EXPLOIT Possible Apache log4j RCE Attempt (tcp corba) (CVE-2021-44228) |
| 2034715     | 2034789      | ET EXPLOIT Possible Apache log4j RCE Attempt (udp corba) (CVE-2021-44228) |
| 2034712     | 2034792      | ET EXPLOIT Possible Apache log4j RCE Attempt (tcp nds) (CVE-2021-44228)   |
| 2034713     | 2034791      | ET EXPLOIT Possible Apache log4j RCE Attempt (udp nds) (CVE-2021-44228)   |
| 2034710     | 2034794      | ET EXPLOIT Possible Apache log4j RCE Attempt (tcp nis) (CVE-2021-44228)   |
| 2034711     | 2034793      | ET EXPLOIT Possible Apache log4j RCE Attempt (udp nis) (CVE-2021-44228)   |


## Bypass and Obfuscation Detection

| Inbound SID | Outbound SID | msg                                                                                                      | Notes    |
|-------------|--------------|----------------------------------------------------------------------------------------------------------|----------|
| 2034659     | 2034781      | ET EXPLOIT Apache log4j RCE Attempt - lower/upper TCP Bypass M1 (CVE-2021-44228)                         |          |
| 2034660     | 2034782      | ET EXPLOIT Apache log4j RCE Attempt - lower/upper UDP Bypass M1 (CVE-2021-44228)                         |          |
| 2034700     | 2034800      | ET EXPLOIT Apache log4j RCE Attempt - lower/upper TCP Bypass M2 (CVE-2021-44228)                         |          |
| 2034701     | 2034799      | ET EXPLOIT Apache log4j RCE Attempt - lower/upper UDP Bypass M2 (CVE-2021-44228)                         |          |
| 2034702     | 2034835      | ET EXPLOIT Apache log4j RCE Attempt - 2021/12/12 Obfuscation Observed (tcp) (CVE-2021-44228)             | Disabled |
| 2034703     | 2034834      | ET EXPLOIT Apache log4j RCE Attempt - 2021/12/12 Obfuscation Observed (udp) (CVE-2021-44228)             | Disabled |
| 2034716     | 2034751      | ET EXPLOIT Possible Apache log4j RCE Attempt - Base64 jndi (tcp) (CVE-2021-44228)                        |          |
| 2034717     | 2034750      | ET EXPLOIT Possible Apache log4j RCE Attempt - Base64 jndi (udp) (CVE-2021-44228)                        |          |
| 2034673     | 2034786      | ET EXPLOIT Possible Apache log4j RCE Attempt - 2021/12/12 Obfuscation Observed M2 (tcp) (CVE-2021-44228) |          |
| 2034674     | 2034805      | ET EXPLOIT Possible Apache log4j RCE Attempt - 2021/12/12 Obfuscation Observed M2 (udp) (CVE-2021-44228) |          |
| 2034671     | 2034836      | ET EXPLOIT Apache log4j RCE Attempt - 2021/12/13 Obfuscation Observed (tcp) (CVE-2021-44228)             | Disabled |
| 2034672     | 2034804      | ET EXPLOIT Apache log4j RCE Attempt - 2021/12/13 Obfuscation Observed (udp) (CVE-2021-44228)             | Disabled |
| 2034676     | 2034806      | ET EXPLOIT Possible Apache log4j RCE Attempt - 2021/12/13 Obfuscation Observed (CVE-2021-44228)          |          |


## AWS Key Disclosure

| Inbound SID | Outbound SID | msg                                                                              |
|-------------|--------------|----------------------------------------------------------------------------------|
| 2034699     | 2034807      | ET EXPLOIT Apache log4j RCE Attempt - AWS Access Key Disclosure (CVE-2021-44228) |


### Nested lower/upper

| Inbound SID | Outbound SID | msg                                                                       |
|-------------|--------------|---------------------------------------------------------------------------|
| 2034706     | 2034798      | ET EXPLOIT Apache log4j RCE Attempt - Nested lower (tcp) (CVE-2021-44228) |
| 2034707     | 2034797      | ET EXPLOIT Apache log4j RCE Attempt - Nested lower (udp) (CVE-2021-44228) |
| 2034708     | 2034796      | ET EXPLOIT Apache log4j RCE Attempt - Nested upper (tcp) (CVE-2021-44228) |
| 2034709     | 2034795      | ET EXPLOIT Apache log4j RCE Attempt - Nested upper (udp) (CVE-2021-44228) |


##  Bypass "Hunting" Rules

| Inbound SID | Outbound SID | msg                                                                                              |
|-------------|--------------|--------------------------------------------------------------------------------------------------|
| 2034661     | 2034783      | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol TCP (CVE-2021-44228)                 |
| 2034662     | 2034784      | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol UDP (CVE-2021-44228)                 |
| 2034663     | 2034785      | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (upper TCP Bypass) (CVE-2021-44228)	 |
| 2034664     | 2034801      | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (upper UDP Bypass) (CVE-2021-44228)  |
| 2034665     | 2034802      | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (lower TCP Bypass) (CVE-2021-44228)  |
| 2034666     | 2034803      | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (lower UDP Bypass) (CVE-2021-44228)  |
| 2034808     |              | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (lower TCP Bypass) (CVE-2021-44228)  |
| 2034809     |              | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (lower UDP Bypass) (CVE-2021-44228)  |
| 2034810     |              | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (upper TCP Bypass) (CVE-2021-44228)  |
| 2034811     |              | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (upper UDP Bypass) (CVE-2021-44228)  |
