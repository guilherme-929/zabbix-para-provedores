FROM debian:12


# Update apt-cache and install Apache
RUN apt update
RUN apt upgrade -y 
RUN apt-get install apache2 libapache2-mod-php php php-mysql php-cli php-pear php-gmp php-gd php-bcmath php-mbstring php-curl php-xml php-zip unzip -y && \
    apt-get -y clean && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm -rf /var/www/html


# Install dumb-init
#ADD https://github.com/Yelp/dumb-init/releases/download/v1.1.2/dumb-init_1.1.2_amd64.deb /tmp
#RUN dpkg -i /tmp/dumb-init_1.1.2_amd64.deb

# Download and extract phpIPAM
ADD https://github.com/phpipam/phpipam/archive/master.zip /tmp
RUN unzip /tmp/master.zip -d /var/www
RUN mv /var/www/phpipam-master /var/www/html
RUN chmod 777 -R /var/www/html/css/images/logo

# Copy default site
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

# Copy phpIPAM configuration
COPY config.php /var/www/html

# Copy cron jobs
COPY phpipam_discoveryCheck /etc/cron.d
COPY phpipam_pingCheck /etc/cron.d
COPY phpipam_resolveIPaddresses /etc/cron.d

RUN a2enmod rewrite

# Apache environment vars
ENV APACHE_LOCK_DIR /var/lock
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2/
ENV APACHE_PID_FILE /var/apache.pid

# phpIPAM Defaults
ENV SSL_ENABLED false
ENV PROXY_ENABLED false

# Expose port(s)
EXPOSE 80 443

ENTRYPOINT ["apache2ctl"]

CMD ["-D", "FOREGROUND"]
#CMD ['/usr/bin/dumb-init', '/usr/sbin/apache2ctl', '-D', 'FOREGROUND']