# Haproxy-fail2ban-example

Example on how Apache2 + Haproxy + fail2ban talk to each other.

## Setup

Haproxy -> fail2ban -> Apache2
-----------------------------
Fail2ban to tackles the log from Haproxy sent to rsyslog which writes it to disk for fail2ban to monitor.
This enables efficient fail2bans even in cases where Haproxy is balacing load to multiple backend instances 
in contrast to running fail2ban on each Apache2 instance separately.
