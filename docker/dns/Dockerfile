FROM alpine:latest as builder

WORKDIR /build

ARG HOSTS="pi.lan=192.168.0.2,win.lan=192.168.0.3,printer.lan=192.168.0.4"
ARG PUBLIC_DNS="86.54.11.1"

# Zainstaluj bash
RUN apk add --no-cache bash

# Wstęp Corefile
RUN printf ".:53 {\n    hosts {\n" > Corefile

# Dodaj wpisy domen/IP
RUN IFS=','; \
    for pair in $(echo "$HOSTS"); do \
        domain=${pair%%=*}; \
        ip=${pair#*=}; \
        printf "        %s %s\n" "$ip" "$domain" >> Corefile; \
    done

# Dokończ Corefile
RUN printf "        fallthrough\n    }\n    forward . $PUBLIC_DNS\n}\n" >> Corefile
# Set permissions for Corefile
RUN chmod 644 Corefile

# Use the official CoreDNS image as the base
FROM coredns/coredns:latest

# Set working directory
WORKDIR /etc/coredns

# Create Corefile directly in the Dockerfile
COPY --from=builder /build/Corefile .

# Expose DNS port
EXPOSE 53/udp
EXPOSE 53/tcp

# Run CoreDNS with the generated Corefile
CMD ["-conf", "Corefile"]
