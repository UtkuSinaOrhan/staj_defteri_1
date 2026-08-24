# Docker Alıştırmaları - Bölüm 1 (Temel İşlemler, Volume ve Bind Mount)

## 1. Temizlik ve Listeleme
Sistemdeki container, imaj ve volume listeleme komutları çalıştırılarak temizlik adımları gerçekleştirildi.
- `docker ps` / `docker image ls` / `docker volume ls`
- Kullanılmayan nesneler prune edilerek temizlendi.

## 2. İmaj Çekme ve Tagleme
- İlgili imajlar çekildi: `centos`, `alpine`, `nginx`, `httpd:alpine`, `ozgurozturknet/adanzyedocker`, `ozgurozturknet/hello-app`, `ozgurozturknet/app1`.
- `docker tag` komutu ile imajlar yeniden etiketlendi ve eskileri silindi.

## 3. Container Yönetimi
- `app1` imajından container oluşturuldu.
- `httpd:alpine` imajından detached container (`httpdalpine-uygulamasi`) ayağa kaldırıldı, logları incelendi (`docker logs`).
- Container durduruldu (`stop`), yeniden başlatıldı (`start`) ve zorla kaldırıldı (`rm -f`).

## 4. Port Publish ve Web Sunucu Uygulaması
- `adanzyedocker:v1` imajından `websunucu` container'ı `-p 80:80` port yönlendirmesiyle başlatıldı.
- `docker exec -it websunucu sh` ile container içine girilerek `/usr/local/apache2/htdocs/index.html` dosyasına ekleme yapıldı.

## 5. Volume ve Bind Mount Alıştırmaları
- `arastirma1` adında volume oluşturuldu (`docker volume create`).
- `birinci`, `ikinci` ve `ucuncu` adında alpine container'ları oluşturularak volume `/test` klasörüne bağlandı (`-v arastirma1:/test`). Read-only (`:ro`) bağlama testi yapıldı.
- Host üzerindeki bir dizin (`~/deneme`) websunucu container'ına bind mount edilerek anlık dosya güncellemeleri test edildi.
