FROM nginx:latest

RUN printf "server {\n\
    listen 80;\n\
    server_name windows;\n\
\n\
    location / {\n\
        proxy_pass http://192.168.0.188:3000;\n\
        proxy_set_header Host \$host;\n\
        proxy_set_header X-Real-IP \$remote_addr;\n\
    }\n\
}\n\
\n\
server {\n\
    listen 80;\n\
    server_name n8n;\n\
\n\
    location / {\n\
        proxy_pass http://192.168.0.190:5678;\n\
        proxy_set_header Host \$host;\n\
        proxy_set_header X-Real-IP \$remote_addr;\n\
    }\n\
}\n" > /etc/nginx/conf.d/default.conf
