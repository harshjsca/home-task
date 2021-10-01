## Overview 

Assuming in scenario 2 the application is being used in server for SSL offloading and proxies around 25000 requests per second is `NGINX`

### Metrics to monitor
1) CPU Stats - SSL Offloading is cpu sensitive process so its important to monitor CPU metrics (user,system,io,nice)
2) Disk Stats - To measure DISK IO of the server while performing Encrytion / Decryption
3) FileSystem - To track the disk space of the server from different partitions
4) loadavg - Load averages can be useful for a quick and dirty idea if a machine has gotten busier (for some definition of busier) recently
5) netstat - Get key network metrics from SSL-offloading or proxy server
6) meminfo - Memory related metrics of server to identify memory issues


#### HOW to do that?
1) Linux system utilities to monitor above metrics 
2) Use mointoring tools like Nagios or Datadog for more detailed logging of NGINX proxy server.
3) Datadog can be used for further detailed monitoring by catagorising metrics into. 

* Basic activity metrics
  - requests per second 
* Error metrics
  - 4xx Codes = Count of client errors such as "403 Forbidden" or "404 Not Found" 
  - 5xx Codes = Count of server errors such as "500 Internal Server Error" or "502 Bad Gateway"
* Performance metrics
  - Request time = Time to process each request, in seconds

#### Challanges of monitoring this?
1) Compatibility metrics for clients: In some cases, the application is not compatible at all with SSL offloading. How to differentiate those clients?
2) HTTPS -> HTTP decryption inspection : HTTP inspection (When encrypted request decrypted by SSL-Offloading server) is difficult to choose (for which http requests)?. Hackers are using the SSL/TLS protocols as a tool to obfuscate their attack payloads. A security device may be able to identify a cross-site scripting or SQL injection attack in plaintext, but if the same attack is encrypted using SSL/TLS, the attack will go through unless it has been decrypted first for inspection.
3) Key Sizes of Requests : As key sizes increases SSL processing will be CPU intensive. How to measure Key sizes?
4) Internet Facing Firewall Monitoring : Catch Security Threats, DDoS attacks , Spoofing.
5) Monitoring of Monitoring and HA of monitoring itself : Its always challenge.