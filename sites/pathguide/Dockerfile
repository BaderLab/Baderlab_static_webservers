FROM ubuntu
#stops apt asking for input during script
ARG DEBIAN_FRONTEND=noninteractive
#updates OS and installs apache2, php8.1, mysql-server, and programs to ensure compatability
RUN apt update ; apt upgrade -y
RUN apt install -y apache2 \
        mysql-server \
        php \
        libapache2-mod-php \
        php-mysql
#copys old files, and start script
COPY ./assets/apache2-configs/ /etc/apache2/
COPY ./assets/site-assets/ /var/www/
COPY ./assets/databases/ /root/
COPY ./assets/start.sh /root/
#configures apache2
RUN a2enmod php8.1
RUN rm -fr /var/www/html/
#starts server
RUN ln -sf /bin/bash /bin/sh
CMD service apache2 start ; service mysql start ; bash /root/start.sh ; cat
EXPOSE 80
