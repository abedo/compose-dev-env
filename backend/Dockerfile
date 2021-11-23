FROM centos:7

ARG BUILD_PHP_VERSION=74

# XDebug configuration
ENV XDEBUG_IDE_KEY=Docker
ENV XDEBUG_REMOTE_HOST=127.0.0.1
ENV XDEBUG_REMOTE_PORT=9000

# Disable application debug mode (consumed by Symfony)
ENV APP_DEBUG=0

# Default application environment (consumed by Symfony)
ENV APPLICATION_ENV="dev"

# Virtual host server name (consumed by nginx)
ENV SERVER_NAME="localhost"

# Allow Composer to run when XDebug is enabled
ENV COMPOSER_ALLOW_XDEBUG=1

# Disable Composer warning about XDebug being enabled
ENV COMPOSER_DISABLE_XDEBUG_WARN=1

# Use hipster editor by default
ENV EDITOR=/usr/bin/vim

# Container user information for running applications safely (not root)
ENV USER_NAME=www
ENV USER_UID=1001
ENV USER_GID=1001

# Install required libraries and tools we will depend on in the following layers
RUN set -ex \
    && yum install -y --setopt=skip_missing_names_on_install=False \
        https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
        http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
        https://repo.percona.com/yum/percona-release-latest.noarch.rpm \
        https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox-0.12.6-1.centos7.x86_64.rpm \
    && yum-config-manager --enable remi remi-safe remi-php${BUILD_PHP_VERSION} \
    && yum install -y --setopt=skip_missing_names_on_install=False \
        bzip2 git mc nano nginx nodejs \
        unzip vim \
        wget zsh \
    && yum -y clean all \
    && rm -rf /tmp/* /var/cache/yum
