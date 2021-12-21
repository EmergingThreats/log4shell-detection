# Overview

The exploitation of CVE-2021-44228 aka "[Log4Shell](https://twitter.com/GossiTheDog/status/1469252646745874435)" 
produces many network artifacts across the various stages required for exploitation. While some methods of exploitation 
can lead to Remote Code Execution (RCE) while other methods result in the disclosure of sensitive information. 

The "path" to RCE can be found detailed in this most excellent graphic by GovCERT.ch  
![](https://www.govcert.admin.ch/blog/zero-day-exploit-targeting-popular-java-library-log4j/assets/log4j_attack.png)  
Image Source: https://www.govcert.admin.ch/blog/zero-day-exploit-targeting-popular-java-library-log4j/

This document details the various network based detection rules created by 
[Emerging Threats](https://twitter.com/ET_Labs).  It will be maintained as new detection rules are updated. 

Please report any false positives or false negatives via [our feedback tool](https://feedback.emergingthreats.net/feedback)

## Download Directions
All rules listed here are [BSD Licensed](https://rules.emergingthreatspro.com/open/suricata-5.0/LICENSE) and can be 
downloaded from rules.emergingthreatspro.com as per the [directions](https://rules.emergingthreatspro.com/OPEN_download_instructions.html)

As updates are still being applied, to ensure receiving the most recent revision of each rule, it is suggested to pull 
the rules directly from the download servers. 

# Exploit Attempts
While these signatures initially provided a good coverage on inbound attempts, attackers were quickly obfuscating the 
payload using an array of different methods including:
- nested lookups
- built-in `lower` and `upper` functions
- hex/oct encoding
- Unicode characters
- "shorthand" notations

An excellent list of Obfuscation and Bypasses can be found via 
[Puliczek/CVE-2021-44228-PoC-log4j-bypass-words](https://github.com/Puliczek/CVE-2021-44228-PoC-log4j-bypass-words)

## Inbound Exploit Attempts
These signatures were created to detect inbound exploit attempts. Additional rules are being created to cover as many 
obfuscation techniques as possible, though the vast array of techniques makes this difficult.  Detection via 
[Post Exploit Activity](#post-exploitation-activity) is a key part of a network based detection strategy.    

### Inbound Signature Deployment Considerations
Inbound signatures are designed to be deployed "in front of" potential vulnerable hosts.  All rules have the 
*destination* host variable set to `[$HOME_NET,$HTTP_SERVERS]`.  In order for these rules to fire correctly, the 
`$HOME_NET` and or `$HTTP_SERVERS` variables _must_ be correctly defined within the IDS Engine's configuration. 

<details><Summary>Click to expand list of 48 Signatures</Summary>

| sid     | msg                                                                                                |
|---------|----------------------------------------------------------------------------------------------------|
| 2034647 | ET EXPLOIT Apache log4j RCE Attempt (http ldap) (CVE-2021-44228)                                   |
| 2034648 | ET EXPLOIT Apache log4j RCE Attempt (http rmi) (CVE-2021-44228)                                    |
| 2034649 | ET EXPLOIT Apache log4j RCE Attempt (tcp ldap) (CVE-2021-44228)                                    |
| 2034650 | ET EXPLOIT Apache log4j RCE Attempt (tcp rmi) (CVE-2021-44228)                                     |
| 2034651 | ET EXPLOIT Apache log4j RCE Attempt (udp ldap) (CVE-2021-44228)                                    |
| 2034652 | ET EXPLOIT Apache log4j RCE Attempt (udp rmi) (CVE-2021-44228)                                     |
| 2034653 | ET EXPLOIT Apache log4j RCE Attempt (udp dns) (CVE-2021-44228)                                     |
| 2034654 | ET EXPLOIT Apache log4j RCE Attempt (tcp dns) (CVE-2021-44228)                                     |
| 2034655 | ET EXPLOIT Apache log4j RCE Attempt (http dns) (CVE-2021-44228)                                    |
| 2034656 | ET EXPLOIT Apache log4j RCE Attempt (udp ldaps) (CVE-2021-44228)                                   |
| 2034657 | ET EXPLOIT Apache log4j RCE Attempt (tcp ldaps) (CVE-2021-44228)                                   |
| 2034658 | ET EXPLOIT Apache log4j RCE Attempt (http ldaps) (CVE-2021-44228)                                  |
| 2034659 | ET EXPLOIT Apache log4j RCE Attempt - lower/upper TCP Bypass M1 (CVE-2021-44228)                   |
| 2034660 | ET EXPLOIT Apache log4j RCE Attempt - lower/upper UDP Bypass M1 (CVE-2021-44228)                   |
| 2034661 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (CVE-2021-44228)                       |
| 2034662 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (CVE-2021-44228)                       |
| 2034663 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol upper Bypass (CVE-2021-44228)          |
| 2034664 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol upper Bypass (CVE-2021-44228)          |
| 2034665 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol lower Bypass (CVE-2021-44228)          |
| 2034666 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol lower Bypass (CVE-2021-44228)          |
| 2034667 | ET EXPLOIT Apache log4j RCE Attempt (udp iiop) (CVE-2021-44228)                                    |
| 2034668 | ET EXPLOIT Apache log4j RCE Attempt (tcp iiop) (CVE-2021-44228)                                    |
| 2034671 | ET EXPLOIT Apache log4j RCE Attempt - 2021/12/13 Obfuscation Observed (CVE-2021-44228)             |
| 2034672 | ET EXPLOIT Apache log4j RCE Attempt - 2021/12/13 Obfuscation Observed (CVE-2021-44228)             |
| 2034673 | ET EXPLOIT Possible Apache log4j RCE Attempt - 2021/12/12 Obfuscation Observed M2 (CVE-2021-44228) |
| 2034674 | ET EXPLOIT Possible Apache log4j RCE Attempt - 2021/12/12 Obfuscation Observed M2 (CVE-2021-44228) |
| 2034676 | ET EXPLOIT Possible Apache log4j RCE Attempt - 2021/12/13 Obfuscation Observed (CVE-2021-44228)    |
| 2034699 | ET EXPLOIT Apache log4j RCE Attempt - AWS Access Key Disclosure (CVE-2021-44228)                   |
| 2034700 | ET EXPLOIT Apache log4j RCE Attempt - lower/upper TCP Bypass M2 (CVE-2021-44228)                   |
| 2034701 | ET EXPLOIT Apache log4j RCE Attempt - lower/upper UDP Bypass M2 (CVE-2021-44228)                   |
| 2034702 | ET EXPLOIT Apache log4j RCE Attempt - 2021/12/12 Obfuscation Observed (CVE-2021-44228)             |
| 2034703 | ET EXPLOIT Apache log4j RCE Attempt - 2021/12/12 Obfuscation Observed (CVE-2021-44228)             |
| 2034706 | ET EXPLOIT Apache log4j RCE Attempt - Nested lower (tcp) (CVE-2021-44228)                          |
| 2034707 | ET EXPLOIT Apache log4j RCE Attempt - Nested lower (udp) (CVE-2021-44228)                          |
| 2034708 | ET EXPLOIT Apache log4j RCE Attempt - Nested upper (tcp) (CVE-2021-44228)                          |
| 2034709 | ET EXPLOIT Apache log4j RCE Attempt - Nested upper (udp) (CVE-2021-44228)                          |
| 2034710 | ET EXPLOIT Possible Apache log4j RCE Attempt (tcp nis) (CVE-2021-44228)                            |
| 2034711 | ET EXPLOIT Possible Apache log4j RCE Attempt (udp nis) (CVE-2021-44228)                            |
| 2034712 | ET EXPLOIT Possible Apache log4j RCE Attempt (tcp nds) (CVE-2021-44228)                            |
| 2034713 | ET EXPLOIT Possible Apache log4j RCE Attempt (udp nds) (CVE-2021-44228)                            |
| 2034714 | ET EXPLOIT Possible Apache log4j RCE Attempt (tcp corba) (CVE-2021-44228)                          |
| 2034715 | ET EXPLOIT Possible Apache log4j RCE Attempt (udp corba) (CVE-2021-44228)                          |
| 2034716 | ET EXPLOIT Possible Apache log4j RCE Attempt - Base64 jndi (CVE-2021-44228)                        |
| 2034717 | ET EXPLOIT Possible Apache log4j RCE Attempt - Base64 jndi (CVE-2021-44228)                        |
| 2034808 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (lower TCP Bypass) (CVE-2021-44228)    | 
| 2034809 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (lower UDP Bypass) (CVE-2021-44228)    |
| 2034810 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (upper TCP Bypass) (CVE-2021-44228)    |  
| 2034811 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (upper UDP Bypass) (CVE-2021-44228)    |   
            
</details>

## Outbound Exploit Attempts
Due to freedom offered in some network environments and the adoption of Log4Shell exploitation by Mirai and other 
botnets, outbound detection has been provided in an attempt to identify systems attempting to exploit Log4Shell 
vulnerabilities from within the "internal" network. These rules are generally the exact same as the inbound signatures 
with the source host variable set to `$HOME_NET`.


### Outbound Signature Deployment Considerations
Outbound signatures are designed to be deployed in a position to alert "internal" systems which are attempting to 
exploit vulnerable hosts either on the internet *or* the "internal" network.  All rules have the *source* host variable 
set to `$HOME_NET` while the *destination* host variable is `any`.  

In order for these rules to fire correctly, the `$HOME_NET` variables _must_ be correctly defined within the IDS 
Engine's configuration.

<details><Summary>Click to expand list of 40 Signatures</Summary>

| sid     | msg                                                                                                           |
|---------|---------------------------------------------------------------------------------------------------------------|
| 2034750 | ET EXPLOIT Possible Apache log4j RCE Attempt - Base64 jndi (Outbound) (CVE-2021-44228)                        |
| 2034751 | ET EXPLOIT Possible Apache log4j RCE Attempt - Base64 jndi (Outbound) (CVE-2021-44228)                        |
| 2034758 | ET EXPLOIT Apache log4j RCE Attempt (http rmi) (Outbound)  (CVE-2021-44228)                                   |
| 2034759 | ET EXPLOIT Apache log4j RCE Attempt (tcp ldap) (Outbound) (CVE-2021-44228)                                    |
| 2034760 | ET EXPLOIT Apache log4j RCE Attempt (tcp rmi) (Outbound) (CVE-2021-44228)                                     |
| 2034761 | ET EXPLOIT Apache log4j RCE Attempt (udp ldap) (Outbound) (CVE-2021-44228)                                    |
| 2034762 | ET EXPLOIT Apache log4j RCE Attempt (udp rmi) (Outbound) (CVE-2021-44228)                                     |
| 2034763 | ET EXPLOIT Apache log4j RCE Attempt (udp dns) (Outbound) (CVE-2021-44228)                                     |
| 2034764 | ET EXPLOIT Apache log4j RCE Attempt (tcp dns) (Outbound) (CVE-2021-44228)                                     |
| 2034765 | ET EXPLOIT Apache log4j RCE Attempt (http dns) (Outbound) (CVE-2021-44228)                                    |
| 2034766 | ET EXPLOIT Apache log4j RCE Attempt (udp ldaps) (Outbound) (CVE-2021-44228)                                   |
| 2034767 | ET EXPLOIT Apache log4j RCE Attempt (tcp ldaps) (Outbound) (CVE-2021-44228)                                   |
| 2034768 | ET EXPLOIT Apache log4j RCE Attempt (http ldaps) (Outbound) (CVE-2021-44228)                                  |
| 2034781 | ET EXPLOIT Apache log4j RCE Attempt - lower/upper TCP Bypass M1 (Outbound) (CVE-2021-44228)                   |
| 2034782 | ET EXPLOIT Apache log4j RCE Attempt - lower/upper UDP Bypass M1 (Outbound) (CVE-2021-44228)                   |
| 2034783 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (Outbound) (CVE-2021-44228)                       |
| 2034784 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol (Outbound) (CVE-2021-44228)                       |
| 2034785 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol upper Bypass (Outbound) (CVE-2021-44228)          |
| 2034786 | ET EXPLOIT Possible Apache log4j RCE Attempt - 2021/12/17 Obfuscation Observed M2 (Outbound) (CVE-2021-44228) |
| 2034787 | ET EXPLOIT Apache log4j RCE Attempt (tcp iiop) (Outbound) (CVE-2021-44228)                                    |
| 2034788 | ET EXPLOIT Apache log4j RCE Attempt (udp iiop) (Outbound) (CVE-2021-44228)                                    |
| 2034789 | ET EXPLOIT Possible Apache log4j RCE Attempt (udp corba) (Outbound) (CVE-2021-44228)                          |
| 2034790 | ET EXPLOIT Possible Apache log4j RCE Attempt (tcp corba) (Outbound) (CVE-2021-44228)                          |
| 2034791 | ET EXPLOIT Possible Apache log4j RCE Attempt (udp nds) (Outbound) (CVE-2021-44228)                            |
| 2034792 | ET EXPLOIT Possible Apache log4j RCE Attempt (tcp nds) (Outbound) (CVE-2021-44228)                            |
| 2034793 | ET EXPLOIT Possible Apache log4j RCE Attempt (udp nis) (Outbound) (CVE-2021-44228)                            |
| 2034794 | ET EXPLOIT Possible Apache log4j RCE Attempt (tcp nis) (Outbound) (CVE-2021-44228)                            |
| 2034795 | ET EXPLOIT Apache log4j RCE Attempt - Nested upper (udp) (Outbound) (CVE-2021-44228)                          |
| 2034796 | ET EXPLOIT Apache log4j RCE Attempt - Nested upper (tcp) (Outbound) (CVE-2021-44228)                          |
| 2034797 | ET EXPLOIT Apache log4j RCE Attempt - Nested lower (udp) (Outbound) (CVE-2021-44228)                          |
| 2034798 | ET EXPLOIT Apache log4j RCE Attempt - Nested lower (tcp) (Outbound) (CVE-2021-44228)                          |
| 2034799 | ET EXPLOIT Apache log4j RCE Attempt - lower/upper UDP Bypass M2 (Outbound) (CVE-2021-44228)                   |
| 2034800 | ET EXPLOIT Apache log4j RCE Attempt - lower/upper TCP Bypass M2 (Outbound) (CVE-2021-44228)                   |
| 2034801 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol upper Bypass (Outbound) (CVE-2021-44228)          |
| 2034802 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol lower Bypass (Outbound) (CVE-2021-44228)          |
| 2034803 | ET HUNTING Possible Apache log4j RCE Attempt - Any Protocol lower Bypass (Outbound) (CVE-2021-44228)          |
| 2034804 | ET EXPLOIT Apache log4j RCE Attempt - 2021/12/17 Obfuscation Observed (Outbound) (CVE-2021-44228)             |
| 2034805 | ET EXPLOIT Possible Apache log4j RCE Attempt - 2021/12/17 Obfuscation Observed M2 (Outbound) (CVE-2021-44228) |
| 2034806 | ET EXPLOIT Possible Apache log4j RCE Attempt - 2021/12/17 Obfuscation Observed (Outbound) (CVE-2021-44228)    |
| 2034807 | ET EXPLOIT Apache log4j RCE Attempt - AWS Access Key Disclosure (Outbound) (CVE-2021-44228)                   |

</details>

# Post Exploitation Activity
While there are many methods of obfuscating the inbound/outbound attack strings, the resulting response traffic can 
be gathered into a few different categories.  

## DNS
One of the more popular attack strings does not deliver any Remote Code Execution(RCE) payload, but instead results in 
exfiltration of sensitive system details via DNS Queries.  

It is not possible to provide high degree of efficacy of log4j exploitation resulting in DNS exfiltration due to the 
dynamic nature of exfiltrated details, large number of "receiving" dns servers. 

DNS Exfiltration is detailed via screenshots in 
[Zander Work's Twitter Thread](https://twitter.com/captainGeech42/status/1470055184449613829)  

### Commonly Observed Callback Domains
There are some commonly used services being observed that are utilized in order to "catch" the exfiltrated data.

Emerging Threats has created the following detections for commonly used Payload and C2 domains. 

| sid     | msg                                                                                                                 |
|---------|---------------------------------------------------------------------------------------------------------------------|
| 2034198 | ET INFO Interactsh Domain in DNS Lookup (.interact .sh)                                                             |
| 2034200 | ET MALWARE Interactsh CnC Activity                                                                                  |
| 2034201 | ET MALWARE Interactsh Control Panel (DNS)                                                                           |
| 2034732 | ET INFO Interactsh Domain in DNS Lookup (.interactsh .com)                                                          |
| 2034669 | ET POLICY dnslog .cn Observed in DNS Query                                                                          |
| 2034670 | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (bindsearchlib .com                        |
| 2034747 | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (rce .ee)                                  |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Security Scanner Domain (log4j .binaryedge .io)            |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Security Scanner Domain (log4shell .huntress .com)         |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Security Scanner Domain (kryptoslogic-cve-2021-44228 .com) |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (ceye .io)                                 |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (oob .li)                                  |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (pwn .af)                                  |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (notburpcollaborator .net)                 |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (scannermcscanface-edgescan .com)          |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (service .exfil .site)                     |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (scanworld .net)                           |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (dns .cyberwar .nl)                        |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (log .exposedbotnets .ru)                  |
| TBD     | ET ATTACK_RESPONSE DNS Query for Observed CVE-2021-44228 Callback Domain (leakix .net)                              |

## LDAP

| sid     | msg                                                                         | Notes                |
|---------|-----------------------------------------------------------------------------|----------------------|
| 2034704 | ET POLICY Anonymous LDAPv3 Bind Request Outbound                            | sets flowbit         |
| 2034705 | ET POLICY Successful Anonymous LDAPv3 Bind Request Outbound                 | depends on `2034704` |
| 2034722 | ET ATTACK_RESPONSE Possible CVE-2021-44228 Payload via LDAPv3 Response      |                      |
| 2034769 | ET ATTACK_RESPONSE Possible CVE-2021-44228 Payload via LDAPv3 Response M2   |                      |
| 2034770 | ET POLICY JavaClass Returned Via Anonymous Outbound LDAPv3 Bind Request     | depends on `2034704` |
| 2034771 | ET POLICY Successful Non-Anonymous LDAPv3 Bind Request Outbound             | sets flowbit         |
| 2034772 | ET POLICY JavaClass Returned Via Non-Anonymous Outbound LDAPv3 Bind Request | depends on `2034771` |
| 2034812 | ET POLICY Non-Anonymous LDAPv3 Bind Request Outbound                        | depends on `2034771` |
| TDB     | ET POLICY Serialized Java Object returned via LDAPv3 Response               |                      |

## LDAPS

| sid     | msg                                                           | Notes                |
|---------|---------------------------------------------------------------|----------------------|
| 2034719 | ET POLICY LDAPSv3 LDAPS_START_TLS Request Outbound            | sets flowbit         |
| 2034720 | ET POLICY Successful LDAPSv3 LDAPS_START_TLS Request Outbound | depends on `2034720` |
| 2034721 | ET POLICY Successful LDAPSv3 LDAPS_START_TLS Request Outbound | depends on `2034720` |

## Java Class Download
These signatures, which have existed for several years, alert on Java downloading additional Class files or Serialized 
Data from a webserver. This method was observed during the initial use of the `jdni:ldap://` attack string which would 
result in the fetching of a payload via HTTP/HTTPS.

| sid     | msg                                                     | Notes                                |
|---------|---------------------------------------------------------|--------------------------------------|
| 2013035 | ET POLICY Java Client HTTP Request                      | sets flowbit for `Java/` User Agent  |
| 2014474 | ET INFO JAVA - Java Class Download                      | depends on `2013035`                 |
| 2014475 | ET INFO JAVA - Java Class Download By Vulnerable Client | See list below for flowbit set rules |
| 2016502 | ET INFO Java Serialized Data via vulnerable client      | See list below for flowbit set rules |
| 2016503 | ET INFO Java Serialized Data                            | depends on `2013035`                 |


### Signatures which determine "Vulnerable Client"
This class of signatures is designed to detect when not using the latest version of a Java "branch" 

| sid     | msg                                               |
|---------|---------------------------------------------------|
| 2011581 | ET POLICY Vulnerable Java Version 1.5.x Detected  |
| 2011582 | ET POLICY Vulnerable Java Version 1.6.x Detected  |
| 2011584 | ET POLICY Vulnerable Java Version 1.4.x Detected  |
| 2014297 | ET POLICY Vulnerable Java Version 1.7.x Detected  |
| 2019401 | ET POLICY Vulnerable Java Version 1.8.x Detected  |
| 2025314 | ET POLICY Vulnerable Java Version 9.0.x Detected  |
| 2025518 | ET POLICY Vulnerable Java Version 10.0.x Detected |
| 2028867 | ET POLICY Vulnerable Java Version 11.0.x Detected |
| 2028868 | ET POLICY Vulnerable Java Version 12.0.x Detected |
| 2028869 | ET POLICY Vulnerable Java Version 13.0.x Detected |
| TBD     | ET POLICY Vulnerable Java Version 14.0.x Detected |
| TBD     | ET POLICY Vulnerable Java Version 15.0.x Detected |
| TBD     | ET POLICY Vulnerable Java Version 16.0.x Detected |
| TBD     | ET POLICY Vulnerable Java Version 17.0.x Detected |
                                                                            

## RMI

| sid     | msg                                                  | Notes                |
|---------|------------------------------------------------------|----------------------|
| 2034718 | ET POLICY RMI Request Outbound                       | sets flowbit         |
| 2034748 | ET POLICY Serialized Java Payload via RMI Response   | depends on `2034748` |
| 2034749 | ET POLICY Unserialized Java Payload via RMI Response | depends on `2034748` |

## IIOP

| sid     | msg                                             | Notes                |
|---------|-------------------------------------------------|----------------------|
| 2034730 | ET POLICY GIOP/IIOP Request Outbound            | sets flowbit         |
| 2034731 | ET POLICY Successful GIOP/IIOP Request Outbound | depends on `2034730` |


# Special Thanks
Emerging Threats would like to thank the following contributors for their efforts:  

For the initial environments for testing   
- [Try Hack Me](https://twitter.com/RealTryHackMe)
- [John Hammond](https://twitter.com/_JohnHammond)

For providing pcaps for signature creation  
- [SLASH30Miata](https://twitter.com/SLASH30Miata)
- Juniper Threat Labs

For tools and directions used in testing environments  
- [vulhub](https://github.com/vulhub/vulhub/blob/ab2cbc517fcabaaf0c8f07a03b7947b795c8dc9a/log4j/CVE-2021-44228/README.md)
- [Veracode](https://github.com/veracode-research/rogue-jndi/)
- [lhotari](https://github.com/lhotari/log4shell-mitigation-tester#exploiting-with-rogue-jndi)  
- [0xJDow](https://github.com/0xJDow/rogue-rmi-server)  
- [christophetd](https://github.com/christophetd/log4shell-vulnerable-app)

For having awesome details which were referenced
- [Puliczek](https://github.com/Puliczek/CVE-2021-44228-PoC-log4j-bypass-words)
- [captainGeech42](https://twitter.com/captainGeech42/)
- [GovCERT.ch](https://www.govcert.admin.ch/blog/zero-day-exploit-targeting-popular-java-library-log4j/#)
