FROM ubuntu

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
        nginx
#RUN apt remove -y r-base \
#        r-base-core
RUN apt autoremove -y
#RUN apt install -y r-base
#RUN apt remove -y r-base

RUN useradd omar -p omar

COPY ./assets/library/ /root/R-library/
COPY ./assets/omar/ /home/omar/
COPY ./assets/mimp /etc/init.d/mimp
COPY ./assets/nginx-configs/ /etc/nginx/

RUN mkdir --parents /root/R/build/
RUN mkdir --parents /root/gcc/build/

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

RUN mv /root/R-library/* /usr/local/lib/R/library/

CMD service mimp start ; service nginx start ; cat
EXPOSE 80
