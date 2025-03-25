FROM mcr.microsoft.com/devcontainers/php:7.4

# Install MariaDB client

RUN apt-get update; export DEBIAN_FRONTEND=noninteractive \
	&& apt-get install -y --no-install-recommends \
	mariadb-client \
	ghostscript \ 
	libavif-dev \
	libfreetype6-dev \
	libicu-dev \
	libjpeg-dev \
	libmagickwand-dev \
	libpng-dev \
	libwebp-dev \
	libzip-dev \
	&& apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd \
	--with-freetype \
	--with-jpeg \
	--with-webp

# RUN	docker-php-ext-install \
# 	mysqli \
# 	pdo \
# 	pdo_mysql

RUN	docker-php-ext-install -j "$(nproc)" \
	bcmath \
	exif \
	gd \
	intl \
	mysqli \
	zip \
	pdo \
	pdo_mysql

# Imagick
RUN curl -fL -o imagick.tgz 'https://pecl.php.net/get/imagick-3.7.0.tgz'; \
	echo '5a364354109029d224bcbb2e82e15b248be9b641227f45e63425c06531792d3e *imagick.tgz' | sha256sum -c -; \
	tar --extract --directory /tmp --file imagick.tgz imagick-3.7.0; \
	grep '^//#endif$' /tmp/imagick-3.7.0/Imagick.stub.php; \
	test "$(grep -c '^//#endif$' /tmp/imagick-3.7.0/Imagick.stub.php)" = '1'; \
	sed -i -e 's!^//#endif$!#endif!' /tmp/imagick-3.7.0/Imagick.stub.php; \
	grep '^//#endif$' /tmp/imagick-3.7.0/Imagick.stub.php && exit 1 || :; \
	docker-php-ext-install /tmp/imagick-3.7.0; \
	rm -rf imagick.tgz /tmp/imagick-3.7.0; 

RUN { \
	# https://www.php.net/manual/en/errorfunc.constants.php
	# https://github.com/docker-library/wordpress/issues/420#issuecomment-517839670
	echo 'error_reporting = E_ERROR | E_WARNING | E_PARSE | E_CORE_ERROR | E_CORE_WARNING | E_COMPILE_ERROR | E_COMPILE_WARNING | E_RECOVERABLE_ERROR'; \
	echo 'display_errors = Off'; \
	echo 'display_startup_errors = Off'; \
	echo 'log_errors = On'; \
	echo 'error_log = /dev/stderr'; \
	echo 'log_errors_max_len = 1024'; \
	echo 'ignore_repeated_errors = On'; \
	echo 'ignore_repeated_source = Off'; \
	echo 'html_errors = Off'; \
	} > /usr/local/etc/php/conf.d/error-logging.ini

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1

