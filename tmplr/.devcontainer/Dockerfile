FROM php:{{ tmplr.php_version }}-apache

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    git \
    python2 \
    libzip-dev \
    unzip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) bcmath gd zip mysqli exif

RUN curl -sL https://deb.nodesource.com/setup_{{ tmplr.node_version }}.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install nodejs
RUN rm nodesource_setup.sh
RUN corepack enable
RUN yarn set version stable
RUN a2enmod rewrite

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer
RUN composer self-update --{{ tmplr.composer_version }}

ENV APACHE_DOCUMENT_ROOT /home/wp/{{ tmplr.project_folder }}{{ tmplr.web_root }}

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN useradd -ms /bin/bash wp

RUN mkdir -p /home/wp/{{ tmplr.project_folder }}
RUN chown -R wp:wp /home/wp/{{ tmplr.project_folder }}