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

#Installs server files (Please contact Gary Bader(gary.bader@utoronto.ca) for server file)
COPY ./pathguide.tgz /pathguide.tgz
RUN tar -cvzf /pathguide.tgz

RUN rm -rf /etc/apache2/*

RUN mv /assets/apache2-configs/* /etc/apache2/
RUN mv /assets/site-assets/* /var/www/
RUN mv /assets/databases/ /root/
RUN mv /assets/start.sh /root/
RUN mv /assets/import.py /import.py
RUN mv /assets/phpmyadmin/* /etc/phpmyadmin/

#RUN rm -r /assets/
#RUN rm /pathguide.tgz

#Configures Apache2
RUN a2enmod php8.1 authz_core authz_host access_compat socache_shmcb slotmem_shm dir
RUN a2ensite 000-default.conf
RUN rm -fr /var/www/html/ /assets
RUN mkdir /var/log/apache2/phpmyadmin/

#Configures PHPMyAdmin
RUN phpenmod mbstring
RUN chown -R www-data:www-data /etc/phpmyadmin/

#Configures server start sequence
CMD service apache2 start ; service mysql start ; bash /root/start.sh ; python3 /import.py ; cat
EXPOSE 80
EXPOSE 8080
