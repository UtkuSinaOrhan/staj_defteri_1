# Staj Günlüğü - 08 Temmuz 2026

## User-Defined Bridge Network (UDBN) ve Log Yönetimi
Docker ağ kurma aşamasında özel köprü ağı (user-defined bridge network) kurma ve kullanma çalışmaları yapıldı. Subnet, IP range ve gateway atanmış UDBN oluşturularak container'lar arasında bağlantı kurma ve koparma işlemleri gerçekleştirildi. Ayrıca log driver çeşitleri incelendi ve log takibi yapıldı.

## Örnek Komutlar ve Kullanımlar

### UDBN Oluşturma ve İnceleme
```bash
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker network create kopru1
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker container run -dit --name websunucu --net kopru1 adanzyedocker:v1 sh
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker container run -dit --name database --net kopru1 adanzyedocker:v1 sh
```

### Özel Subnet, IP Range ve Gateway Atama
```bash
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker network create --driver=bridge --subnet=10.10.0.0/16 --ip-range=10.10.10.0/24 --gateway=10.10.10.10 kopru2
```

### Network Bağlantı Ekleme / Çıkarma ve Silme
```bash
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker network connect kopru2 database
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker network disconnect kopru2 database
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker network rm kopru2
```

### Nginx Log Takibi ve Log Komutları
- `docker logs con1`: Temel log görüntüleme.
- `docker logs --details con1`: Detaylı loglama.
- `docker logs -t con1`: Zaman damgalı loglama.
- `docker logs --until [zaman] con1`: Belirtilen zamana kadar olan loglar.
- `docker logs --since [zaman] con1`: Belirtilen zamandan sonraki loglar.
- `docker logs --tail [sayı] con1`: Sondan istenen sayıda log.
- `docker logs -f con1`: Canlı log takibi.
- `docker info`: Sistem genelindeki desteklenen logging driver'ları listeler (`awslogs`, `fluentd`, `gcplogs`, `gelf`, `journald`, `json-file`, `local`, `splunk`, `syslog`). Varsayılan driver `json-file`'dır.