FROM php:8.1-fpm-alpine

# تثبيت nginx و supervisor
RUN apk add --no-cache nginx supervisor

# نسخ ملفات الموقع
COPY . /var/www/html

# إعداد nginx ليمرر ملفات PHP إلى php-fpm
# مع استبدال المنفذ 80 بالمنفذ الديناميكي PORT عند بدء التشغيل
RUN echo $'server { \n\
    listen 80; \n\
    root /var/www/html; \n\
    index index.php index.html; \n\
    location / { \n\
        try_files $uri $uri/ /index.php?$query_string; \n\
    } \n\
    location ~ \.php$ { \n\
        fastcgi_pass 127.0.0.1:9000; \n\
        fastcgi_index index.php; \n\
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name; \n\
        include fastcgi_params; \n\
    } \n\
}' > /etc/nginx/http.d/default.conf \
&& echo $'[supervisord] \n\
nodaemon=true \n\
\n\
[program:php-fpm] \n\
command=php-fpm \n\
autostart=true \n\
autorestart=true \n\
\n\
[program:nginx] \n\
command=/bin/sh -c "sed -i \'s/listen 80;/listen \'$PORT\';/\' /etc/nginx/http.d/default.conf && nginx -g \'daemon off;\'" \n\
autostart=true \n\
autorestart=true' > /etc/supervisord.conf

EXPOSE 80
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
