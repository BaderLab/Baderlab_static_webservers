FROM ubuntu:latest

# Install the necessary programs
RUN apt update ; apt -y upgrade
RUN apt install -y apache2 \
        python2 \
        python-pip
#RUN pip2 install libsvm-official

# Install files from previos server
COPY ./assets/html/ /var/www/html/
COPY ./assets/cgi-bin/ /usr/lib/cgi-bin/
COPY ./assets/lib-files/ /usr/local/lib/python2.7/dist-packages/

# Configurate apache2
RUN a2enmod cgid
RUN echo "AddHandler cgi-script .cgi .py"
RUN chmod 755 /usr/lib/cgi-bin/*.py

# Initalization script
EXPOSE 80
CMD /etc/init.d/apache2 start ; cat
RUN ln -sf /bin/bash /bin/sh
