# Copyright (C) 2020  Matthew "strager" Glazar
# See end of file for extended copyright information.

FROM ubuntu:22.04

RUN apt-get update && \
        DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
          apache2 \
          libapache2-mod-php \
          php-fpm \
          php-mysql && \
    rm /etc/apache2/sites-available/*.conf /etc/apache2/sites-enabled/*.conf

COPY apache2/apache2.conf apache2/envvars apache2/ports.conf /etc/apache2/
COPY apache2/mods-available/*.conf /etc/apache2/mods-available/
COPY apache2/sites-available/*.conf /etc/apache2/sites-available/
COPY run-apache2.sh /tmp/run-apache2.sh

RUN a2ensite \
        001-quicklintjs \
        002-admin.quick-lint-js.com \
        003-c.quick-lint-js \
        003-quick-lint-js.com && \
    a2enconf \
        php8.1-fpm && \
    a2dismod \
        mpm_event && \
    a2enmod \
        expires \
        headers \
        http2 \
        mpm_prefork \
        rewrite \
        ssl

EXPOSE 80/tcp 443/tcp
# Keep in sync with create-dev-certificates.sh.
ENV DEV_TLD=.developer.app

CMD ["/tmp/run-apache2.sh"]

# quick-lint-js finds bugs in JavaScript programs.
# Copyright (C) 2020  Matthew "strager" Glazar
#
# This file is part of quick-lint-js.
#
# quick-lint-js is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# quick-lint-js is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with quick-lint-js.  If not, see <https://www.gnu.org/licenses/>.
