FROM alpine:3.18

# Install Apache
RUN apk --no-cache add apache2

# Enable mod_rewrite
RUN sed -i 's/#LoadModule rewrite_module/LoadModule rewrite_module/' /etc/apache2/httpd.conf

# Install build dependencies and gettext
RUN apk --no-cache add build-base autoconf libtool m4 re2c bison wget gettext gettext-dev libxml2 libxml2-dev libintl

# Install cURL and its development libraries
RUN apk --no-cache add curl curl-dev

WORKDIR /usr/src

# Download PHP 5.4 source code
RUN wget https://www.php.net/distributions/php-5.4.45.tar.gz
RUN tar -xzvf php-5.4.45.tar.gz

# Build and install PHP 5.4
WORKDIR /usr/src/php-5.4.45
RUN ./configure \
    --prefix=/usr/local/php \
    --with-config-file-path=/usr/local/php/etc \
    --with-mysql=mysqlnd \
    --with-mysqli=mysqlnd \
    --with-pdo-mysql=mysqlnd \
    --enable-cli \
    --enable-mbstring \
    --enable-zip \
    --with-gettext \
    --with-libxml-dir=/usr/include/libxml2 \
    --with-curl \
    --enable-json
RUN make
RUN make install

# Cleanup
RUN rm -rf /usr/src/php-5.4.45*
RUN apk del build-base autoconf libtool m4 re2c bison wget gettext gettext-dev libxml2-dev

# Set the PATH to include PHP binary
ENV PATH="/usr/local/php/bin:${PATH}"

# Create a PHP configuration directory
RUN mkdir -p /usr/local/php/etc

# Copy a basic PHP.ini file (you may want to customize this)
COPY php.ini /usr/local/php/etc/php.ini

WORKDIR /var/www/html

# Expose port 80 (or the port your application is running on)
EXPOSE 80

# Start Apache in the foreground
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
