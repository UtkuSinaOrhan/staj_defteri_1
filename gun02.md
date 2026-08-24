# Staj Günlüğü - 06 Temmuz 2026

## Docker Volume Kavramı
- **Tanım:** Volume, container ve image gibi bir Docker objesidir. Image veya container yaratır gibi oluşturulurlar.
- **Özellikler:** 
  - Docker daemon'ın kurulu olduğu host makine üzerinde kurulurlar (istenirse cloud gibi çeşitli volume driverları kullanılabilir).
  - Container içinde dahili bir klasör gibi görünürler, bu sebeple kullanımda sorun yaratmazlar.
  - Bir volume birden fazla container'a bağlanabilir.

## Temel Volume Komutları ve Sözdizimi
- `docker volume create [VOLUME_NAME]`: Yeni bir volume oluşturur.
- `docker volume inspect [VOLUME_NAME]`: Volume detaylarını gösterir.
  - `Mountpoint` satırı, volume içine kaydedilen verilerin host üzerinde bulunduğu klasörü gösterir.
- `docker container run -it -v ilkvolume:/uygulama alpine sh`: 
  - `-it` ile interaktif bağlantı açılır, `-v` ile volume bağlanır. Container içindeki `/uygulama` klasörüne `ilkvolume` bağlanır ve Alpine imajı ile container yaratılarak shell açılır.
- `docker volume ls`: Aktif volume'leri listeler.
- `docker container run -it -v ilkvolume:/deneme3:ro centos sh`: 
  - Volume, container'a `read-only` (salt okunur) olarak bağlanır. İçeride dosya oluşturulmak istendiğinde hata alınır (`touch: cannot touch 'test.txt': Read-only file system`).

## Bind Mount İşlemi
Udemy ve yapay zeka yardımıyla container ile host arasında dosya paylaşımı (bind mount) sağlandı. Localde yapılan değişiklikler container içinde de güncel olarak değişmektedir.

**Örnek Kodlar:**
```bash
utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker -v
Docker version 29.6.1, build 8900f1d

utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker container run -d -p 80:80 -v /mnt/c/Users/UtkuSinaOrhan/Desktop/AdanZyeDocker-master/kisim3/bolum28/websitesi:/usr/share/nginx/html nginx 
dc5e96f41fe2651223458bf01f1d4e7f03c01fb0af4bad02788fc04ef769ca83

utkusinaorhan@ASUS-TUF-GAMING-F15:~$ docker rm -f dc5  # Container silme komutu
dc5
```

## Alıştırmalar
Konu tekrarı alıştırmaları yapıldı. Kodlarda zorlanan ve hatırlanmayan `exec` gibi komutlar yapay zeka aracılığıyla pekiştirildi.