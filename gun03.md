# Staj Günlüğü - 07 Temmuz 2026

## Docker Network Driverlar ve Port Publish
Docker network driver'ları, port publish kavramının ne olduğu, ne zaman ve ne amaçla kullanılacakları öğrenilerek ilgili alıştırmalar yapıldı. Bu süreçte Udemy ve yapay zeka içeriklerinden faydalanıldı.

## Terminal Komutları ve Çıktıları

### 1. Network Listesi ve İnceleme
```bash
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
d390715a3a47   bridge    bridge    local
3a743a540fef   host      host      local
cc0e45756174   none      null      local

utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker network inspect bridge
```
*(Bridge ağı altında Subnet `172.17.0.0/16` ve Gateway `172.17.0.1` değerleri incelendi.)*

### 2. Bridge Driver ve Container İletişimi
```bash
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker container run -d adanzyedocker:v1
7a00aa11be5c40d6bcd6bc47f4710ad97038fe4cd3827f00bc77d330732f9dd6

utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker exec -it 7a00 sh
/usr/src/myapp # ifconfig
/usr/src/myapp # ping 8.8.8.8
```
*Not: Aynı bridge network'e bağlı container'lar birbiriyle doğrudan iletişim kurabilir.*

### 3. Host Driver (`--net host`)
Ana Linux kernel IP adresi ile container IP adresi aynı paylaşılır:
```bash
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker container run -it --name deneme1 --net host adanzyedocker:v1 sh
```

### 4. None Driver (`--net none`)
Herhangi bir ağ bağlantısının bulunmadığı izole ortam:
```bash
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker container run -it --name deneme2 --net none adanzyedocker:v1 sh
/usr/src/myapp # ping 8.8.8.8
connect: Network unreachable
```

### 5. Port Publish
Host üzerindeki bir portun container portuna yönlendirilmesi:
```bash
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker container run -d --publish 8080:80 adanzyedocker:v1
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker ps
```