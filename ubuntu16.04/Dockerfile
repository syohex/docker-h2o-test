# Start from Debian Jessie
FROM ubuntu:16.04
MAINTAINER Syohei YOSHIDA

RUN apt-get -y update && apt-get -y upgrade

# Install packages
RUN apt-get -y \
    install build-essential autoconf automake libtool cmake cmake-data php-cgi git wget curl \
    cpanminus libipc-signal-perl liblist-moreutils-perl libwww-perl libio-socket-ssl-perl zlib1g-dev \
    apache2-utils libev-dev libxml2-dev openssl libssl-dev zlib1g-dev libcunit1-dev libspdylay-dev \
    ruby ruby-dev rake bison python libpython-dev libuv1 libuv1-dev nghttp2 libnghttp2-dev libgnutls-dev

# Perl modules
RUN cpanm -n Net::EmptyPort Scope::Guard Plack FCGI FCGI::ProcManager Starlet \
             JSON Path::Tiny Test::Exception

# Install curl with nghttp2
RUN curl -L https://curl.haxx.se/download/curl-7.50.0.tar.gz | tar xzf - \
    && (cd curl-7.50.0 && ./configure --with-nghttp2 --disable-shared && make && make install)

# Update ld.so cache
RUN ldconfig
