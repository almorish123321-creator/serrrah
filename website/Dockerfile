FROM php:8.1-cli

WORKDIR /app
COPY . /app

# إنشاء سكربت بدء التشغيل الذي يقرأ المنفذ من متغير البيئة PORT
RUN echo '#!/bin/sh' > /start.sh && \
    echo 'exec php -S 0.0.0.0:${PORT:-80} -t /app' >> /start.sh && \
    chmod +x /start.sh

EXPOSE 80

CMD ["/start.sh"]
