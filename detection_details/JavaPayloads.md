# Log4Shell Java Class Payload Downloads
During the RCE path for Log4Shell attempts, it is common to see the vulnerable application request a Java Payload from 
a webserver.  The signatures detailed below attempt to detect this behavior.   

# Example Traffic
![](Java_Class_Download/download.png)

# Detection Logic
In order to detect outbound requests for a Java Class, a flowbit will be used to first identify an outbound request 
from Java, with a Class file or a Serialized object returned. It is important to note that this is not indicate malicous 
traffic, however given this behavior in the Log4Shell RCE path, alerts from these signatures, with great attention paid 
to the [Class Download Rules](#class-response-rules), warrant investigation. 

## Java Client HTTP Requests
These signatures are designed to set a flowbit on an HTTP Request by a Java application as determined by the User-Agent 
of the request. 

| sid     | msg                                               | Example UA        | Flowbit Set                   | Alerting | 
|---------|---------------------------------------------------|-------------------|-------------------------------|----------|
| 2013035 | ET POLICY Java Client HTTP Request                | `Java/`           | ET.http.javaclient            | False    |
| 2011581 | ET POLICY Vulnerable Java Version 1.5.x Detected  | `Java/1.5.0`      | ET.http.javaclient.vulnerable | True     |
| 2011582 | ET POLICY Vulnerable Java Version 1.6.x Detected  | `Java/1.6.0_210`  | ET.http.javaclient.vulnerable | True     |
| 2011584 | ET POLICY Vulnerable Java Version 1.4.x Detected  | `Java/1.4.0`      | ET.http.javaclient.vulnerable | True     |
| 2014297 | ET POLICY Vulnerable Java Version 1.7.x Detected  | `Java/1.7.0_300.` | ET.http.javaclient.vulnerable | True     |
| 2019401 | ET POLICY Vulnerable Java Version 1.8.x Detected  | `Java/1.8.0_290`  | ET.http.javaclient.vulnerable | True     |
| 2025314 | ET POLICY Vulnerable Java Version 9.0.x Detected  | `Java/9.0`        | ET.http.javaclient.vulnerable | True     |
| 2025518 | ET POLICY Vulnerable Java Version 10.0.x Detected | `Java/10.0.0`     | ET.http.javaclient.vulnerable | True     |
| 2028867 | ET POLICY Vulnerable Java Version 11.0.x Detected | `Java/11.0.12`    | ET.http.javaclient.vulnerable | True     |
| 2028868 | ET POLICY Vulnerable Java Version 12.0.x Detected | `Java/12.0.1`     | ET.http.javaclient.vulnerable | True     |
| 2028869 | ET POLICY Vulnerable Java Version 13.0.x Detected | `Java/13.0.1`     | ET.http.javaclient.vulnerable | True     |
| 2034814 | ET POLICY Vulnerable Java Version 14.0.x Detected | `Java/14.0.1`     | ET.http.javaclient.vulnerable | True     |
| 2034815 | ET POLICY Vulnerable Java Version 15.0.x Detected | `Java/15.0.1`     | ET.http.javaclient.vulnerable | True     |
| 2034816 | ET POLICY Vulnerable Java Version 16.0.x Detected | `Java/16.0.1`     | ET.http.javaclient.vulnerable | True     |
| 2034817 | ET POLICY Vulnerable Java Version 17.0.x Detected | `Java/17.0.0`     | ET.http.javaclient.vulnerable | True     |


## Class Response Rules                                                              
The following rules depend on either `ET.http.javaclient.vulnerable` or `ET.http.javaclient` to be set on the outgoing 
response

| sid     | msg                                                     | Flowbit Required              | Detection Screenshot                       | 
|---------|---------------------------------------------------------|-------------------------------|--------------------------------------------|
| 2014474 | ET INFO JAVA - Java Class Download                      | ET.http.javaclient            | [2014474](Java_Class_Download/2014474.png) |
| 2014475 | ET INFO JAVA - Java Class Download By Vulnerable Client | ET.http.javaclient.vulnerable | [2014475](Java_Class_Download/2014475.png) |
| 2016502 | ET INFO Java Serialized Data via vulnerable client      | ET.http.javaclient.vulnerable |                                            |
| 2016503 | ET INFO Java Serialized Data                            | ET.http.javaclient            |                                            |


