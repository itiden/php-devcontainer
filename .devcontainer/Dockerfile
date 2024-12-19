FROM php:{{ tmplr.php_version }}-apache

ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USER_NAME=wp
ENV GROUP_NAME=wp

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    curl \
    git \
    libzip-dev \
    unzip \
    libwebp-dev \ 
    libavif-dev \
    default-mysql-client \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp --with-avif \
    && docker-php-ext-install -j$(nproc) bcmath gd zip mysqli exif pdo pdo_mysql

RUN curl -fsSL https://deb.nodesource.com/setup_{{ tmplr.node_version }}.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install nodejs
RUN rm nodesource_setup.sh
RUN corepack enable
ENV COREPACK_ENABLE_DOWNLOAD_PROMPT=0

RUN a2enmod rewrite

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer
RUN composer self-update --{{ tmplr.composer_version }}

ENV APACHE_DOCUMENT_ROOT /home/wp/{{ tmplr.project_folder }}{{ tmplr.web_root }}

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# Add WP-CLI 
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar
RUN mv wp-cli.phar /usr/local/bin/wp

RUN groupadd -g $GROUP_ID $GROUP_NAME
RUN useradd -ms /bin/bash $USER_NAME -u $USER_ID -g $GROUP_NAME

RUN mkdir -p /home/wp/{{ tmplr.project_folder }}
RUN chown -R wp:wp /home/wp/{{ tmplr.project_folder }}
RUN chmod -R 775 /home/wp/{{ tmplr.project_folder }}