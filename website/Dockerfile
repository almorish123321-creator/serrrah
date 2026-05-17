FROM php:8.1-apache

# تفعيل mod_rewrite لروابط نظيفة
RUN a2enmod rewrite

# نسخ جميع ملفات الموقع
COPY . /var/www/html

# ضبط الصلاحيات
RUN chown -R www-data:www-data /var/www/html

# سيستخدم Apache المنفذ من متغير البيئة PORT تلقائياً
# لا حاجة لتغيير أي شيء، Railway سيحقن المنفذ تلقائياً في Apache

EXPOSE 80
