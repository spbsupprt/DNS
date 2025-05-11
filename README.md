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


