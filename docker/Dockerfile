FROM wordpress:php8.4-fpm

RUN groupadd -g 1000 appgroup && \
useradd -u 1000 -g appgroup -m appuser || true

RUN chown -R www-data:www-data /var/www/html

USER www-data

EXPOSE 9000
