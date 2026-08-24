# Docker Alıştırmaları - Bölüm 3 (Docker Hub, Dockerfile ve Multi-stage Build)

## 1. Docker Hub İşlemleri
- `docker login` ve `docker logout` komutları ile kimlik doğrulama işlemleri yapıldı.
- Docker Hub üzerinde `alistirma` adında public bir repository oluşturuldu.

## 2. İmaj Çekme ve Tagleme
- `centos:7`, `ubuntu:latest`, `ubuntu:18.04`, `ubuntu:20.04`, `alpine:latest`, `nginx:latest`, `nginx:alpine` imajları çekildi.
- `ubuntu:18.04` imajı `utkusinaorhan/alistirma:ubuntu` olarak etiketlenip Docker Hub'a gönderildi (`docker push`).

## 3. Özel Dockerfile Yazımı ve Build İşlemi
- `nginx:latest` baz alınarak özel bir `Dockerfile` hazırlandı:
  - `LABEL` ile geliştirici bilgisi eklendi.
  - `ENV KULLANICI=utkusinaorhan` ve `ARG RENK` tanımlandı.
  - `curl`, `htop`, `wget` paketleri kuruldu.
  - WordPress arşivi (`latest.tar.gz`) eklendi (`ADD`).
  - `HEALTHCHECK` ve `ENTRYPOINT` tanımlamaları yapıldı.
- Build argümanları kullanılarak `kirmizi` ve `sari` etiketli iki ayrı imaj üretildi ve port yönlendirmeleriyle test edildi.

## 4. Multi-stage Build Uygulaması
- Java konsol uygulamasını derlemek için `eclipse-temurin:8-jdk-alpine` (derleme aşaması) ve çalıştırmak için `eclipse-temurin:8-jre-alpine` (çalıştırma aşaması) kullanan `Dockerfile.multi` dosyası yazıldı.
- İmaj build edilerek (`utkusinaorhan/alistirma:java`) container üzerinden çalıştırıldı ve Docker Hub'a yüklendi.
