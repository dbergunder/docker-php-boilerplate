FROM php:7.4-fpm-alpine

ARG TIMEZONE=${TIMEZONE:-America/Chicago}

RUN apk add --update --no-cache \
    coreutils \
    curl \
    libzip-dev \
    zip \
    git

RUN docker-php-ext-install zip && docker-php-ext-enable zip

RUN apk add --no-cache $PHPIZE_DEPS \
    && echo no | pecl install redis \
    && docker-php-ext-enable redis

# Install Composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
&& composer --version

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone \
&& printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini \
&& "date"

COPY settings.ini /usr/local/etc/php/conf.d/
COPY settings.ini /usr/local/etc/php/cli/conf.d/
COPY php-fpm.pool.conf /usr/local/etc/php/php-fpm.d/

CMD ["php-fpm"]
