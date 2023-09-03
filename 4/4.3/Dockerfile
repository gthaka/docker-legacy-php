# Use the Ubuntu 14.04 slim image as the base
FROM ubuntu:14.04

# Update the system
RUN apt-get update && apt-get upgrade -y

# Install Apache2
RUN apt-get install -y apache2 apache2-dev

# Install necessary packages to build PHP
RUN apt-get install -y build-essential libxml2-dev wget flex perl

# Download PHP 4.3 source code
RUN wget https://museum.php.net/php4/php-4.3.11.tar.gz --no-check-certificate

# Extract the source code
RUN tar xzvf php-4.3.11.tar.gz

# Go to the PHP source code directory
WORKDIR /php-4.3.11

# Configure the build
RUN ./configure --with-apxs2=/usr/bin/apxs2

# Compile and install PHP
RUN make && make install

# Expose port 80 for Apache
EXPOSE 80

# Start Apache in the foreground
CMD ["apachectl", "-D", "FOREGROUND"]
