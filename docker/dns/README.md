# DNS

This directory contains a simple DNS server implementation for local network resolution.

## Installation

To set up the DNS server, you can use the following commands:

(Docker is required for this setup)

```bash
curl https://raw.githubusercontent.com/Bajdzis/local-network/refs/heads/master/docker/dns/Dockerfile -o Dockerfile
docker build --build-arg HOSTS="my.domain=192.168.0.2,my.domain2=192.168.0.4" -t dns .
docker run -d --restart always --name dns -p 53:53/udp -p 53:53/tcp dns
```

## Build arguments

- `HOSTS`: A comma-separated list of hostnames and their corresponding IP addresses. For example, `my.domain=192.168.0.2,my.domain2=192.168.0.4`.
- `PUBLIC_DNS`: (Optional) A public DNS server to forward queries to if the hostname is not found in the local configuration. Defaults to `86.54.11.1`.
