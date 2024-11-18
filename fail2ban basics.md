---
tags: [f2b,fail2ban]
---


```bash
# Show all jails configured, by default only "sshd" is.
fail2ban-client status

# List IP's currently banned to connect to sshd:
fail2ban-client status sshd
```

```bash
# Manually ban IP address
fail2ban-client set sshd banip 192.168.0.10

# Manually un-ban IP address
fail2ban-client set sshd unbanip 192.168.0.10
```


```bash

# Show the IP's actually filtered by iptables.
#
# When no IP's are banned yet, it is possible that this shows an error
# saying the table does not exist.
# 
iptables -L f2b-sshd -n
```

None of the above commands show when an IP address was banned or when it will be
un-banned. That information can be found in the log file
`/var/log/fail2ban.log`
