![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of shame (2020-10-13)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
54.38.81.231|ns31251136.ip-54-38-81.eu|8
217.182.192.217|ns3073700.ip-217-182-192.eu|8
51.75.144.43|ns3129517.ip-51-75-144.eu|8
62.102.148.68|-|8
192.42.116.22|this-is-a-tor-exit-node-hviv122.hviv.nl|8
104.244.75.153|-|8
209.95.51.11|nyc-exit.privateinternetaccess.com|8
77.247.181.165|politkovskaja.torservers.net|8
185.191.126.212|-|8
145.239.92.26|relay3.tor.ian.sh|8
94.102.56.238|-|8
51.195.148.18|relay2.tor.ian.sh|8
185.220.102.247|185-220-102-247.torservers.net|7
185.220.102.241|185-220-102-241.torservers.net|7
185.220.102.248|tor-exit-relay-2.anonymizing-proxy.digitalcourage.de|7
198.251.83.73|tor-exit-04.nonanet.net|7
104.244.75.53|-|7
176.10.104.240|tor1e1.digitale-gesellschaft.ch|7
185.220.101.207|-|7
104.244.77.95|-|7
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|7
192.42.116.14|this-is-a-tor-exit-node-hviv114.hviv.nl|7
185.220.101.211|-|7
185.220.101.213|-|7
51.77.135.89|ns31066279.ip-51-77-135.eu|7
162.247.74.74|wiebe.tor-exit.calyxinstitute.org|7
185.220.101.15|-|7
85.209.0.101|-|7
91.250.242.12|-|7
171.25.193.77|tor-exit1-readme.dfri.se|7
171.25.193.78|tor-exit4-readme.dfri.se|7
185.220.101.9|-|7
185.220.101.1|-|7
18.27.197.252|wholesomeserver.media.mit.edu|7
51.75.64.187|relay4.tor.ian.sh|7
185.220.102.8|185-220-102-8.torservers.net|7
171.25.193.20|tor-exit0-readme.dfri.se|7
176.10.99.200|accessnow.org|7
185.220.102.254|tor-exit-relay-8.anonymizing-proxy.digitalcourage.de|7
23.160.208.246|relay13f.tor.ian.sh|7
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|7
185.220.101.146|-|7
185.220.102.250|tor-exit-relay-4.anonymizing-proxy.digitalcourage.de|7
185.220.101.200|-|7
