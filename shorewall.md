---
tags: [shorewall,iptables,tun,vpn,openconnect]
---

To make sure shorewall allows multiple `tun` devices so more than one VPN
connections are supported by the shorewall config, use a wildcard `+` for the
`tun` interface definition.

`/etc/shorewall/interfaces`

```ascii
?FORMAT 2
net enp0s31f6 tcpflags,logmartians,nosmurfs
net tun+ tcpflags,logmartians,nosmurfs
```
