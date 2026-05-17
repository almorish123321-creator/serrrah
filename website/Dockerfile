FROM php:8.1-apache

# إصلاح مشكلة "More than one MPM loaded"
RUN a2dismod mpm_event && a2enmod mpm_prefork

# تفعيل mod_rewrite
RUN a2enmod rewrite

# نسخ جميع ملفات الموقع
COPY . /var/www/html

# الصلاحيات
RUN chown -R www-data:www-data /var/www/html
