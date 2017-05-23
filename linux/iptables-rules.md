IPTables Rules
======

## Index

1. [Blocking and Logging IP Addresses](#blocking-and-logging-ip-addresses)
2. [Viewing Blocked IP Addresses](#viewing-blocked-ip-addresses-in-iptables)
3. [Searching for a Blocked IP Address](#searching-for-a-blocked-ip-address-in-iptables)
4. [Deleting Blocked IP Addresses](#deleting-blocked-ip-addresses)

Blocking and Logging IP Addresses in IPTables
------

In order to turn on kernel logging of matching packets with the target of your log file use these two commands:
```bash
/sbin/iptables -i {adapter i.e. eth0} -A INPUT -s {IP Address} -j LOG --log-prefix "IP DROPPED IN IPTABLES:"
/sbin/iptables -i {adapter i.e. eth0} -A INPUT -s {IP Address} -j DROP
```

Viewing Blocked IP Addresses in IPTables
------

IPTables is ridiculously powerful for such a small program. To get just the IP Addresses that are blocked use this command:

```bash
/sbin/iptables -L INPUT -v -n
```

The result should look something like this:
```bash
Chain INPUT (policy ACCEPT 1346K packets, 577M bytes)
 pkts bytes target     prot opt in     out     source               destination
20543 1240K LOG        all  --  eth0   *       1.1.1.1       0.0.0.0/0            LOG flags 0 level 4 prefix "IP DROP SPOOF A:"
20505 1236K DROP       all  --  eth0   *       1.1.1.1       0.0.0.0/0
```
    
Searching For a Blocked IP Address in IPTables
------

The best way to find a blocked IP Address in IPTables is to use grep. Using the command above, we will pipe (|) and use grep like so:

```bash
/sbin/iptables -L INPUT -v -n | grep 1.1.1.1
```

That will give you output similar to this:
```bash
20543 1240K LOG        all  --  eth0   *       113.195.145.52       0.0.0.0/0            LOG flags 0 level 4 prefix "IP DROP SPOOF A:"
20505 1236K DROP       all  --  eth0   *       113.195.145.52       0.0.0.0/0
```

Deleting Blocked IP Addresses
------

In order to delete blocked IP Addresses, you'll just need to use this command:
```bash
iptables -D INPUT -s 1.1.1.1 -j DROP
```