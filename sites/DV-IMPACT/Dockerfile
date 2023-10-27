FROM ubuntu

ARG DEBIAN_FRONTEND=noninteractive

#Updates & Installs required programs
RUN apt update ; apt upgrade -y
RUN apt install -y apache2 \
        mysql-server \
        php \
        libapache2-mod-php \
        php-mysql \
        wget \
        python3 \
        phpmyadmin

#Installs server files (Please contact Gary Bader(gary.bader@utoronto.ca) for server files)
COPY ./prm-db.tgz /prm-db.tgz
RUN tar -cvzf /prm-db.tgz
RUN rm -rf /etc/apache2/*

RUN mv /assets/apache2-configs/* /etc/apache2/
RUN mv /assets/phpmyadmin/* /etc/phpmyadmin/
RUN mv /assets/site-assets/* /var/www/
RUN mv /assets/databases/ /root/
RUN mv /assets/start.sh /root/
RUN mv /assets/import.py /import.py

RUN rm -rf /assets/ /prm-db.tgz

#Configures Apache2
RUN a2enmod php8.1 authz_core authz_host access_compat socache_shmcb slotmem_shm dir
RUN a2ensite default.conf
RUN rm -fr /var/www/html/

#Configures PHPMyAdmin
RUN phpenmod mbstring
RUN chown -R www-data:www-data /etc/phpmyadmin/

#Configures server startup sequence
CMD service apache2 start ; service mysql start ; sh /root/start.sh ; python3 /import.py ; cat
EXPOSE 80
EXPOSE 8080
