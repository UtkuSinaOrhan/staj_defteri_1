FROM nginx:latest

LABEL maintainer="Utku Sina Orhan <utkusinaorhan0@gmail.com>"

ENV KULLANICI=utkusinaorhan

ARG RENK

RUN apt-get update && apt-get install -y \
    curl \
    htop \
    wget \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /gecici
ADD https://wordpress.org/latest.tar.gz /gecici/

WORKDIR /usr/share/nginx/html
COPY html/${RENK}/ .

RUN chmod +x ./script.sh

HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 \
  CMD curl -f http://localhost/ || exit 1

ENTRYPOINT ["./script.sh"]