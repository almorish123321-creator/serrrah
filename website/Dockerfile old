FROM php:8.1-apache

RUN a2enmod rewrite

COPY . /var/www/html
RUN chown -R www-data:www-data /var/www/html

# استبدال منفذ 80 بمنفذ Railway الديناميكي عند بدء التشغيل
RUN echo 'ServerName localhost' >> /etc/apache2/apache2.conf
RUN sed -i 's/80/${PORT}/g' /etc/apache2/sites-available/000-default.conf /etc/apache2/ports.conf

# تعديل أمر بدء Apache ليستبدل المتغير PORT فعلياً
CMD ["/bin/bash", "-c", "sed -i \"s/\\(Listen \\)80/\\1$PORT/\" /etc/apache2/ports.conf && sed -i \"s/\\(VirtualHost \\*:\\)80/\\1$PORT/\" /etc/apache2/sites-available/000-default.conf && apache2-foreground"]
