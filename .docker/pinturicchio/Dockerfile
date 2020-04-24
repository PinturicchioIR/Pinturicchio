FROM php:7.4-fpm-alpine

RUN echo -e "\e[32m > Install core dependencies\e[0m"
RUN apk add --no-cache --update bash curl freetype-dev libjpeg-turbo-dev libpng-dev

RUN echo -e "\e[32m > Install PHP extensions\e[0m"
RUN apk add --no-cache --update --virtual .phpize-deps $PHPIZE_DEPS \
    && docker-php-ext-install bcmath gd pdo_mysql \
    && pecl install redis \
	&& docker-php-ext-enable redis \
	# Install XDebug only on dev environment
	&& pecl install xdebug && docker-php-ext-enable xdebug \
    && docker-php-source delete \
	&& apk del .phpize-deps

RUN echo -e "\e[32m > PHP modules\e[0m"
RUN php -m

RUN echo -e "\e[32m > Install Composer\e[0m"
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
