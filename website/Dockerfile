FROM php:8.1-apache

# تفعيل mod_rewrite لروابط نظيفة
RUN a2enmod rewrite

# نسخ جميع ملفات الموقع
COPY . /var/www/html
RUN chown -R www-data:www-data /var/www/html

# إعداد سكربت بدء التشغيل الذي يستبدل المنفذ 80 بـ PORT
RUN echo '#!/bin/sh' > /usr/local/bin/start.sh && \
    echo 'if [ -z "$PORT" ]; then PORT=80; fi' >> /usr/local/bin/start.sh && \
    echo 'sed -i "s/Listen 80/Listen $PORT/" /etc/apache2/ports.conf' >> /usr/local/bin/start.sh && \
    echo 'sed -i "s/<VirtualHost \*:80>/<VirtualHost \*:$PORT>/" /etc/apache2/sites-available/000-default.conf' >> /usr/local/bin/start.sh && \
    echo 'exec apache2-foreground' >> /usr/local/bin/start.sh && \
    chmod +x /usr/local/bin/start.sh

EXPOSE 80

CMD ["/usr/local/bin/start.sh"]
