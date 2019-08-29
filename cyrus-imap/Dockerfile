FROM ubuntu:bionic 

RUN apt-get update 
RUN export TZ="Europe/Berlin"
RUN echo "cyrus-common cyrus-common/removespools boolean true" | debconf-set-selections
RUN echo "postfix postfix/mailname string your.hostname.com" | debconf-set-selections
RUN echo "postfix postfix/main_mailer_type string 'Internet Site'" | debconf-set-selections

RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq postfix  sasl2-bin cyrus-imapd cyrus-clients cyrus-doc cyrus-admin 

RUN mkdir -p /run/cyrus/proc && chown -R cyrus /run/cyrus

ADD cyrus.conf /etc/cyrus.conf
ADD imapd.conf /etc/imapd.conf

# create some default use, cyrus is configured as admin in imapd.conf
RUN echo "cyrus"|saslpasswd2 -u test -c cyrus -p
RUN echo "bob"|saslpasswd2 -u test -c bob -p
RUN echo "alice"|saslpasswd2 -u test -c alice -p


ENTRYPOINT /bin/sh


