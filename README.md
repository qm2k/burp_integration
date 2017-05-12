# Integration files for [BURP](http://burp.grke.org/)

## Usage
Please _don't_ blindly copy these files to your `/etc` directory, read them and make sure they do what you want.
Read [prerequisites](#prerequisites) section before proceeding and correct files accordingly if your system is different.

## Prerequisites
- BURP service user is called `burp`
- BURP is configured to log to syslog

## File descriptions

### etc/logrotate.d/burp
Rotates BURP logs montly, keeps 12 most recent.

### etc/rsyslog.d/30-burp.conf
Write burp logs to `/var/log/burp/burp.log` instead of `/var/log/syslog`.

### etc/tmpfiles.d/burp-server.conf
Creates empty file `/var/run/burp-server.pid` belonging to user `burp` at boot.

### etc/fail2ban/filter.d/burp-auth.conf
Filter that catches "unable to authorise on server" and "check cert failed on server" messages in log.

### etc/fail2ban/jail.burp
Enables `burp-auth` filter for `/var/log/burp/burp.log`, blocks ports 4971 and 4972 when triggered.
Include contents of this file to your `/etc/fail2ban/jail.local`.

