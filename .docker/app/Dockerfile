FROM php:7.1-apache

# Install dependencies
# PS: individual RUN blocks allow individual caches, in case some of them fail
RUN apt-get update
RUN apt-get install -y git
RUN apt-get install -y zlib1g-dev

# Install the extensions themselves
RUN docker-php-ext-install pdo_mysql
RUN pecl install xdebug
RUN docker-php-ext-install zip

# Enable them
RUN docker-php-ext-enable pdo_mysql
RUN docker-php-ext-enable xdebug
RUN docker-php-ext-enable zip

# Enable Apache modules
RUN a2enmod rewrite

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
