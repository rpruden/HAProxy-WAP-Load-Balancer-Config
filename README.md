# HAProxy-WAP-Load-Balancer-Config
This is an HA Proxy config file for load balancing Web Application Proxy servers

While setting up HAProxy as a load balancer for WAP I found that monitoring the health was tricky.
I was finally able to get monitoring to work in a fashion that only marks the server as healthy if
the ADFS service is running. Previously, reboots of the WAP server would result in error 501 during
the time when the server booted until the services actually started. HAProxy was unaware of this
and therefore would route traffic to it before it was ready. Using this config I have been able to
prevent HAProxy from erroneously marking the destination server as up until the ADFS service is running.

To use this config, you will want to replace the strings "adfs.domain.com" and "wap.domain.com" with the domain name of your ADFS farm and WAP farm respectiely.

This will tell the health check to connect to your WAP server's IP address without verifying SSL certificate and using SNI to indicate the proper ADFS hostname.
