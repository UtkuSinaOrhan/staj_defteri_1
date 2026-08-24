# Udemy Docker Eğitimi Notları

## Bölüm 2: Giriş ve Temel Kavramlar
- **Container Teknolojisi:** İzole, hafif ve taşınabilir süreçler çalıştırmak için kullanılır.
- **Gerekli Ön Bilgiler:**
  - Temel bilgisayar kullanım bilgisi
  - Linux OS konsepti
  - Linux shell (kabuk) kullanımı
  - Temel network bilgisi

### Linux Shell
- **Navigasyon ve Dosya İşlemleri:**
  - `pwd`: Print Working Directory - Bulunulan dizini gösterir.
  - `ls -la`: Bulunulan klasördeki tüm dosyaları (gizliler dahil) detaylı ve izinleriyle listeler.
  - `cd <klasör_adı>`: Klasör değiştirmeyi sağlar.
  - `mkdir <klasör_adı>`: Yeni bir klasör oluşturur.
- **Dosya Okuma ve Düzenleme:**
  - `cat <dosya_adı>`: Küçük dosyaların içeriğini hızlıca terminale basar.
  - `tail -f <dosya_adı>`: Dosyanın son satırını canlı olarak takip eder (Docker loglarını izlerken bu mantık kullanılır).
  - `nano <dosya_adı>`: Terminal içinde çalışan basit bir metin editörüdür.
- **Sistem ve Süreç Takibi:**
  - `ps aux` / `top`: Arka planda çalışan süreçleri listeler.
  - `grep`: Büyük çıktılar içinde arama yapmayı sağlar (örn: `ps aux | grep node`).

### Temel Network Mantığı
- **IP Adresi ve Localhost:**
  - `127.0.0.1` ve `localhost` kendi bilgisayarını (host) temsil eder.
  - **Docker Tuzağı:** Docker container'ı içindeyken `localhost` denildiğinde container kendi içine bakar, ana bilgisayara değil.
- **Port Mantığı:**
  - `80 / 443`: Standart web trafiği (HTTP / HTTPS)
  - `3306`: MySQL veritabanı portu
  - `5432`: PostgreSQL veritabanı portu
- **Port Forwarding / Mapping:** Container dış dünyaya kapalıdır; dışarıdan erişim için port yönlendirmesi (`-p 8080:3000`) yapılır.

---

## Bölüm 4: İşletim Sistemi Mimarisi
- İşletim sistemleri **Kernel (Çekirdek)**, **UI (Arayüz)** ve **Apps (Uygulamalar)** olmak üzere 3 bileşenden oluşur.
- **Kernel:** Fiziksel altyapı ile uygulama arasındaki işlemleri yürüten, sistem kaynaklarını yöneten ana bileşendir.

---

## Bölüm 5: Sanallaştırma (Virtualization)
- **Server:** Hizmet sunar; güçlü ve yüksek kapasiteli işlem gücüne sahiptir, uzun süreli ve kesintisiz çalışmak üzere tasarlanmıştır.
- **Client:** Hizmeti kullanır; görece düşük kapasiteli işlem gücüne sahiptir, tek kullanıcıya yöneliktir.

---

## Bölüm 6: Container ve İzolasyon
- **Container Nedir?** Uygulamanın çalışması için gereken kod, kütüphane ve bağımlılıkları tek paket haline getiren izole hafif bir süreçtir. Sfırdan OS kurmaz, host OS'in kernel'ini paylaşır.
- **Namespaces (İzolasyon):**
  - `PID Namespace`: Süreç izolasyonu (PID 1 olarak görünür).
  - `NET Namespace`: Ağ kartı, IP ve port tablosu izolasyonu.
  - `MNT Namespace`: Dosya sistemi izolasyonu.
  - `UTS Namespace`: Hostname izolasyonu.
- **Control Groups (Cgroups):** Kaynak (CPU ve RAM) sınırlaması sağlar.
- **Layered File System (UnionFS):** İmajlar read-only katmanlardan oluşur; container çalıştırıldığında en üste ince bir read-write katman eklenir.

---

## Bölüm 7 & 8 & 9: Docker Engine, Image ve Container
- **Docker Engine Mimarisi:** Docker CLI (Komut satırı), REST API ve Docker Daemon (`dockerd`).
- **Image vs Container:** Image, read-only şablondur; container ise bu şablonun çalışan kopyasıdır.

---

## Bölüm 26: Docker Volume
- Container ve image gibi bir Docker objesidir. Host üzerinde veya cloud driver'larda saklanabilir. Birden fazla container'a bağlanabilir.
- **Komutlar:**
  - `docker volume create [VOLUME_NAME]`
  - `docker volume inspect [VOLUME_NAME]` (`Mountpoint` verilerin fiziksel yerini gösterir).
  - `docker container run -it -v ilkvolume:/uygulama alpine sh`
  - `docker volume ls`
  - `docker container run -it -v ilkvolume:/deneme3:ro centos sh` (Read-only bağlantı).

---

## Bölüm 27: Bind Mounts
- Host üzerindeki bir klasör veya dosyanın container içine map edilmesidir. Verileri kalıcı kılmak veya dosya paylaşmak için kullanılır.

---

## Bölüm 31 & 32: Docker Plugin ve Network Driver'lar
- **Network Driver Türleri:**
  - `Bridge`: Varsayılan ağ sürücüsü.
  - `Host`: Host ağ yığını doğrudan paylaşılır.
  - `MacVlan`: Container'lara fiziksel ağda kendi MAC adresini verir.
  - `None`: Ağ bağlantısı yoktur.
  - `Overlay`: Farklı host'lardaki container'ları birbirine bağlar.

---

## Bölüm 34: Port Publish
- Belirtilen port üzerindeki istekleri container'a yönlendirir (`-p 8080:80`).

---

## Bölüm 35: User-Defined Bridge Network (UDBN)
- Özel köprü ağları oluşturarak container'ların isimleri (`service name`) üzerinden birbirleriyle DNS çözümlemesi ile haberleşmesini sağlar.

---

## Bölüm 36: Docker Logging
- Loglama ve akış yönetimi (`stdout`, `stderr`).
- **Komutlar:** `docker logs`, `--details`, `-t`, `--since`, `--until`, `--tail`, `-f`.
- Desteklenen log driver'lar: `json-file` (varsayılan), `local`, `syslog`, `journald`, vb.

---

## Bölüm 39 & 40: Docker Stats, Top ve Kaynak Sınırlandırma
- `docker top`: Çalışan süreçleri gösterir.
- `docker stats`: Anlık CPU, RAM ve I/O tüketimini listeler.
- `--memory="100MiB"`, `--cpus="1.5"`, `--cpuset-cpus="0,3"` ile kaynak kısıtlaması yapılır.

---

## Bölüm 41: Environment Variables
- Çevresel değişken tanımlama ve aktarma (`--env`, `--env-file`).

---

## Bölüm 45 & 46 & 47: Docker Image, Hub ve Dockerfile Talimatları
- **Image İsimlendirme:** `registry/repository:tag`
- **Dockerfile Başlıca Talimatları:** `FROM`, `LABEL`, `RUN`, `WORKDIR`, `USER`, `COPY`, `ADD`, `ENV`, `ARG`, `VOLUME`, `EXPOSE`, `ENTRYPOINT`, `CMD`, `HEALTHCHECK`, `SHELL`.

---

## Bölüm 56 & 57 & 59 & 60 & 61 & 62: İleri Düzey Docker Konuları
- **Exec ve Shell Form:** `CMD ["echo", "$TEST"]` (Exec) vs `CMD echo $TEST` (Shell).
- **Multi-stage Build:** Çok aşamalı imaj derleme ile imaj boyutlarını küçültme.
- **Build ARG:** Build aşamasında değişken tanımlama (`--build-arg`).
- **Docker Commit:** Çalışan container'dan imaj üretme.
- **Docker Save / Load:** İmajları arşivleme (`.tar`) ve taşıma.
- **Docker Registry:** Kendi yerel imaj deponuzu kurma.

---

## Bölüm 66: Docker Compose
- Çoklu container mimarilerini `docker-compose.yml` dosyası ile tek komutla yönetme (`docker compose up`, `down`, `build`, vb.).

---

## Bölüm 69 & 70 & 73 & 75 & 78 & 79: Docker Swarm ve Orkestrasyon
- **Docker Swarm:** Cluster yönetimi, manager ve worker node'lar.
- **Docker Service:** Replicated ve global servis modları, scaling ve rolling update (`docker service update`, `rollback`).
- **Overlay Network:** Çoklu sunucu arası iletişim ağı.
- **Docker Secret:** Hassas verilerin şifrelenerek güvenli yönetimi.
- **Docker Stack:** `docker stack deploy` ile compose dosyalarını Swarm üzerinde çalıştırma.
