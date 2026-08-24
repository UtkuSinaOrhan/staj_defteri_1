# Docker Alıştırmaları - Bölüm 2 (Network, Loglar ve Kaynak Yönetimi)

## 1. Kullanıcı Tanımlı Bridge Network (UDBN)
- Subnet (`10.10.0.0/16`), IP range (`10.10.10.0/24`) ve gateway (`10.10.10.10`) tanımlı `alistirma-agi` adında özel köprü ağı oluşturuldu:
  ```bash
  docker network create --subnet 10.10.0.0/16 --ip-range 10.10.10.0/24 --gateway 10.10.10.10 alistirma-agi
  ```
- `nginx:1.16` imajından `web1` container'ı bu ağa bağlanarak 8080 portundan yayınlandı.

## 2. Log Takibi
- `docker logs web1` ve `docker logs -f web1` (follow) komutları ile HTTP istekleri ve 404 hataları canlı olarak izlendi.

## 3. Ağ Bağlantısı Ekleme ve İletişim
- `test1` container'ı default bridge ağında başlatıldıktan sonra `docker network connect alistirma-agi test1` komutu ile ikinci bir ağa bağlandı.
- Container içinden `ping web1` ile DNS ve IP tabanlı iletişim test edildi.

## 4. CPU ve Memory Kısıtlamaları ile Çoklu Servis
- `websrv` (web kayıt uygulaması) maksimum 2 CPU ve 80 portu ile `alistirma-agi` üzerinde başlatıldı.
- `mysqldb` veritabanı container'ı maksimum 1 GB RAM sınırı (`--memory=1g`) ve çevre değişkeni dosyalarıyla (`--env-file`) ayağa kaldırıldı.
- Form doldurma ve dosya yükleme testleri başarıyla tamamlandı.
