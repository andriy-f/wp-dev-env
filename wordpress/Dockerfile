FROM wordpress:php8.3-apache

# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
	&& apt-get -y install --no-install-recommends git openssh-client less msmtp

# Install wp-cli 2.12.0
RUN cd ~/ \
	&& curl -L -o wp-cli.phar "https://github.com/wp-cli/wp-cli/releases/download/v2.12.0/wp-cli-2.12.0.phar" \
	&& echo "be928f6b8ca1e8dfb9d2f4b75a13aa4aee0896f8a9a0a1c45cd5d2c98605e6172e6d014dda2e27f88c98befc16c040cbb2bd1bfa121510ea5cdf5f6a30fe8832 *wp-cli.phar" | sha512sum -c - \
	&& mv wp-cli.phar /usr/local/bin/wp \
	&& chmod +x /usr/local/bin/wp

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1

