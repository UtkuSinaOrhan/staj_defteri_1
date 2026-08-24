# Dockerfile Talimatları ve Açıklamaları

- **FROM:** Oluşturulacak imajın hangi temel imajdan türetileceğini belirtir. Dockerfile içinde geçmesi zorunlu **tek** talimattır.  
  *Örn:* `FROM ubuntu:18.04`

- **LABEL:** İmaj metadata'sına `key=value` şeklinde etiketler ekler.  
  *Örn:* `LABEL version="1.0.8"`

- **RUN:** İmaj oluşturulurken (`build` aşamasında) terminalde komut çalıştırır.  
  *Örn:* `RUN apt-get update`

- **WORKDIR:** Çalışma dizinini değiştirir (`cd` komutunun karşılığıdır).  
  *Örn:* `WORKDIR /usr/src/app`

- **USER:** Komutların hangi kullanıcı yetkisiyle çalıştırılacağını belirler.  
  *Örn:* `USER poweruser`

- **COPY:** Host üzerindeki dosya veya klasörleri imaj içine kopyalar.  
  *Örn:* `COPY /source /usr/src/app`

- **ADD:** `COPY` ile aynı işi yapar ancak ek olarak uzak URL'lerden dosya indirmeye ve `.tar` arşivlerini otomatik açarak kopyalamaya izin verir.  
  *Örn:* `ADD https://wordpress.org/latest.tar.gz /temp`

- **ENV:** İmaj içinde kalıcı environment variable (çevresel değişken) tanımlar.  
  *Örn:* `ENV TEMP_FOLDER="/temp"`

- **ARG:** Sadece imaj oluşturma (`build`) aşamasında geçerli değişkenler tanımlar. İmaj çalışırken (runtime) bu değişkenler bulunmaz.  
  *Örn:* `ARG VERSION="1.0"`

- **VOLUME:** İmaj içerisinde bir mount point (bağlantı noktası) tanımlar.  
  *Örn:* `VOLUME /myvol`

- **EXPOSE:** Container'ın hangi portlar üzerinden dışarıya hizmet vereceğini belirtir (bilgilendirme amaçlıdır).  
  *Örn:* `EXPOSE 80/tcp`

- **ENTRYPOINT:** Container başlatıldığında çalıştırılacak ana uygulamayı ve yürütülebilir dosyayı ayarlar.  
  *Örn:* `ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]`

- **CMD:** Container başlatıldığında varsayılan olarak çalıştırılacak argümanları veya komutu belirler.  
  *Örn:* `CMD ["java", "merhaba"]`

- **HEALTHCHECK:** Container'ın sağlığını (çalışıp çalışmadığını) periyodik olarak kontrol eder.  
  *Örn:* `HEALTHCHECK --interval=5m --timeout=3s CMD curl -f http://localhost/ || exit 1`

- **SHELL:** Komutların çalıştırılacağı kabuk ortamını değiştirir.  
  *Örn:* `SHELL ["powershell", "-command"]`