#
# Dockerfile for phpBB
#

FROM php:5.6-apache
MAINTAINER kev<noreply@datageek.info>

RUN apt-get update && apt-get install -y curl unzip bzip2 libpq-dev libpng12-dev libjpeg-dev \
        && rm -rf /var/lib/apt/lists/* \
        && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
        && docker-php-ext-install gd mysqli pgsql

WORKDIR /var/www/html

ENV PHPBB_VERSION 3.1.4
ENV PHPBB_URL https://www.phpbb.com/files/release/phpBB-${PHPBB_VERSION}.tar.bz2
ENV PHPBB_SHA512 cc13d34679d987b7c956999b273b109fd441dcc786d7612c4b726423d674ade5
ENV PHPBB_FILE phpBB.tar.bz2

RUN curl -fSL ${PHPBB_URL} -o ${PHPBB_FILE} \
        && echo "${PHPBB_SHA512} ${PHPBB_FILE}" | sha256sum -c - \
        && tar -xjf ${PHPBB_FILE} --strip-components=1 \
        && rm ${PHPBB_FILE} \
        && chown -R www-data:www-data .

