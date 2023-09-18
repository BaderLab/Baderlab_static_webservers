FROM ubuntu

RUN HOST_IP=""

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update ; apt upgrade -y
RUN apt install -y openjdk-8-jre \
        openjdk-8-jdk \
        libcurl4-openssl-dev \
        wget \
        gcc \
        g++ \
        gfortran \
        make \
        r-base \
        libicu-dev \
        gcc-multilib \
        flex \
        autogen \
        nginx \
        apache2 \
        mysql-server \
        php \
        libapache2-mod-php \
        php-mysql \
        python2 \
        python-pip \
        libapache2-mod-wsgi-py3
RUN apt autoremove -y

RUN useradd omar -p omar

COPY ./assets/site-assets/ /var/www/
COPY ./assets/cgi-bin/ /usr/lib/cgi-bin/
COPY ./assets/apache2-configs/ /etc/apache2/
COPY ./assets/databases/ /root/databases/
COPY ./assets/start.sh /root/start.sh
COPY ./assets/library/ /root/R-library/
COPY ./assets/omar/ /home/omar/
COPY ./assets/mimp /etc/init.d/mimp
COPY ./assets/nginx-configs/ /etc/nginx/
COPY ./assets/wikiconfig.py /usr/local/share/moin/server/
COPY ./assets/htdocs/ /usr/lib/cgi-bin/htdocs/
COPY ./assets/moin.cgi /usr/local/share/moin/server/moin2.cgi
COPY ./assets/lib-files/ /usr/local/lib/python2.7/dist-packages/

RUN chown -R www-data:www-data /var/www/mywiki/
RUN wget http://static.moinmo.in/files/moin-1.9.11.tar.gz -O /root/moin.tgz
RUN tar -xvzf /root/moin.tgz -C /root/

WORKDIR /root/moin-1.9.11/
RUN python2 setup.py install --prefix='/usr/local' --record=install.log
RUN mv /usr/local/share/moin/server/moin2.cgi /usr/local/share/moin/server/moin.cgi

RUN mkdir --parents /root/R/build/
RUN mkdir --parents /root/gcc/build/

RUN a2ensite POW.conf PRM.conf DV-IMPACT.conf pathguide.conf greet.conf moin.conf
RUN a2enmod php8.1
RUN a2dissite 000-default.conf
RUN rm -fr /var/www/html/
RUN mkdir /var/log/apache2/PRM/ /var/log/apache2/POW/ /var/log/apache2/DV-IMPACT/ /var/log/apache2/pathguide/ /var/log/apache2/greet
RUN a2enmod cgid
RUN chmod 755 /usr/lib/cgi-bin/*.py

RUN wget https://cran.r-project.org/src/base/R-3/R-3.6.3.tar.gz -O /root/R/R-3.6.3.tar.gz
RUN tar -xvzf /root/R/R-3.6.3.tar.gz -C /root/R/
RUN wget https://github.com/gcc-mirror/gcc/archive/refs/tags/releases/gcc-9.4.0.tar.gz -O /root/gcc/gcc-9.4.0.tar.gz
RUN tar -xvzf /root/gcc/gcc-9.4.0.tar.gz -C /root/gcc/

RUN cp -r /home/omar/lib/play-2.2.1/* /usr/bin/
RUN chown -R omar:omar /home/omar/

WORKDIR /root/gcc/gcc-releases-gcc-9.4.0/
RUN /root/gcc/gcc-releases-gcc-9.4.0/contrib/download_prerequisites
WORKDIR /root/gcc/9.4/build
RUN /root/gcc/gcc-releases-gcc-9.4.0/configure --enable-multilib --disable-libsanitizer --disable-libcilkrts
RUN make
RUN make check
RUN make install

WORKDIR /home/omar/mimp_webserver/
RUN /home/omar/lib/play-2.2.1/play compile

WORKDIR /root/R/R-3.6.3/
RUN ./configure --with-readline=no --with-x=no
RUN make
RUN make install

WORKDIR /root/

RUN mv /root/R-library/* /usr/local/lib/R/library/

CMD service apache2 start ; service mysql start ; service mimp start ; service nginx start ; bash /root/start.sh ; cat

EXPOSE 80-86
