# Nginx

This directory contains a simple Nginx reverse proxy configuration for local network services.

## Installation

```bash
curl https://raw.githubusercontent.com/Bajdzis/local-network/refs/heads/master/docker/nginx/Dockerfile -o Dockerfile
docker build -t nginx .
docker run -d --restart always --name nginx -p 80:80 nginx
```

