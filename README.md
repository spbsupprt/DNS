# DNS

- Что нужно сделать?

- взять стенд https://github.com/erlong15/vagrant-bind

- добавить еще один сервер client2

- завести в зоне dns.lab

имена

- web1 - смотрит на клиент1

- web2 смотрит на клиент2

- завести еще одну зону newdns.lab

- завести в ней запись

- www - смотрит на обоих клиентов

- настроить split-dns

- клиент1 - видит обе зоны, но в зоне dns.lab только web1

- клиент2 видит только dns.lab

  ---

Дано:

![image](https://github.com/user-attachments/assets/a40ea71b-8cb8-417e-b384-8de78b2dc097)


Выполняем плейбук:

https://github.com/spbsupprt/DNS/blob/main/dns.yml


![image](https://github.com/user-attachments/assets/2b3cdb7a-5602-45d4-9ef3-bcd3440195e4)


# 1. Проверка зон на DNS-серверах
На ns01 (master):

```
$ sudo named-checkconf
(нет вывода - конфигурация корректна)

$ sudo named-checkzone dns.lab /etc/named/named.dns.lab
zone dns.lab/IN: loaded serial 2711201407
OK

$ sudo named-checkzone dns.lab /etc/named/named.dns.lab.client
zone dns.lab/IN: loaded serial 2711201407
OK

$ sudo named-checkzone newdns.lab /etc/named/named.newdns.lab
zone newdns.lab/IN: loaded serial 2711201007
OK
```


# 2. Проверки с client1

```
$ dig @192.168.50.10 web1.dns.lab +short
192.168.50.15

$ dig @192.168.50.10 web2.dns.lab +short
(нет вывода)

$ dig @192.168.50.10 www.newdns.lab +short
192.168.50.15
192.168.50.16

$ ping -c 2 web1.dns.lab
PING web1.dns.lab (192.168.50.15) 56(84) bytes of data.
64 bytes from client (192.168.50.15): icmp_seq=1 ttl=64 time=0.012 ms
64 bytes from client (192.168.50.15): icmp_seq=2 ttl=64 time=0.045 ms

$ ping -c 2 web2.dns.lab
ping: web2.dns.lab: Name or service not known
```
