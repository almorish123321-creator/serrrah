FROM php:8.1-apache

# تفعيل mod_rewrite إذا كان الموقع يحتاج روابط نظيفة
RUN a2enmod rewrite

# نسخ جميع ملفات الموقع إلى مجلد Apache
COPY . /var/www/html

# تغيير الصلاحيات (اختياري)
RUN chown -R www-data:www-data /var/www/html

EXPOSE 80
