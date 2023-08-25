FROM ubuntu

RUN apt update ; apt -y upgrade
RUN apt install -y apache2 \
        python2 \
        wget \
        libapache2-mod-wsgi-py3

COPY ./assets/site-assets/ /var/www/
COPY ./assets/apache2-config/ /etc/apache2/
COPY ./assets/wikiconfig.py /usr/local/share/moin/server/
COPY ./assets/htdocs/ /usr/lib/cgi-bin/htdocs/
COPY ./assets/moin.cgi /usr/local/share/moin/server/moin2.cgi

RUN rm -r /var/www/html/
RUN chown -R www-data:www-data /var/www/mywiki/
RUN wget http://static.moinmo.in/files/moin-1.9.11.tar.gz -O /root/moin.tgz
RUN tar -xvzf /root/moin.tgz -C /root/
RUN a2enmod cgid ; a2dissite 000-default ; a2ensite moin

WORKDIR /root/moin-1.9.11/
RUN python2 setup.py install --prefix='/usr/local' --record=install.log
RUN mv /usr/local/share/moin/server/moin2.cgi /usr/local/share/moin/server/moin.cgi

CMD service apache2 start ; cat
EXPOSE 80
