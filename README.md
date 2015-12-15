# BIRD

Simple Ansible playbook for the Internet routing daemon [BIRD](http://bird.network.cz/)

* Supports **OSPF** for route distribution
* Supports **BFD** for failure detencion
* For ``Debian`` and ``FreeBSD`` only

## Routes
```
172.29.29.0/24     via 172.27.27.6 on tap0 [ospf1 13:59:22] * I (150/20) [172.27.27.6]
172.31.31.0/24     via 172.27.27.4 on tap0 [ospf1 13:59:22] * I (150/20) [172.27.27.4]
172.24.24.0/24     via 172.27.27.5 on tap0 [ospf1 13:59:22] * I (150/20) [172.27.27.5]
172.27.27.0/24     dev tap0 [ospf1 13:59:22] * I (150/10) [172.27.27.7]
172.26.26.0/24     dev tun0 [ospf1 2015-12-01] * I (150/10) [172.27.27.1]
```

## OSPF
```
router 172.27.27.1
  distance 0
  network 172.27.27.0/24 metric 10
  stubnet 172.26.26.0/24 metric 10

router 172.27.27.2
  distance 10
  network 172.27.27.0/24 metric 10

router 172.27.27.3
  distance 10
  network 172.27.27.0/24 metric 10

router 172.27.27.4
  distance 10
  network 172.27.27.0/24 metric 10
  stubnet 172.31.31.0/24 metric 10

router 172.27.27.5
  distance 10
  network 172.27.27.0/24 metric 10
  stubnet 172.24.24.0/24 metric 10

router 172.27.27.6
  distance 10
  network 172.27.27.0/24 metric 10
  stubnet 172.29.29.0/24 metric 10

router 172.27.27.7
  distance 10
  network 172.27.27.0/24 metric 10
```

## TO-DO
- [ ] Working IPv6 infrastructure
- [ ] OpenWRT deploying
