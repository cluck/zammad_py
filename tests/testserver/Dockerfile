FROM ubuntu:20.04
WORKDIR /root

RUN ln -nsf /usr/share/zoneinfo/Europe/Zurich /etc/timezone
RUN apt-get clean && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install locales ca-certificates wget curl gnupg apt-transport-https
RUN locale-gen en_US.UTF-8 ; echo "LANG=en_US.UTF-8" >/etc/default/locale && \
    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | gpg --dearmor >/etc/apt/trusted.gpg.d/elasticsearch-oss.gpg && \
    wget -qO - https://dl.packager.io/srv/zammad/zammad/key | gpg --dearmor >/etc/apt/trusted.gpg.d/pkgr-zammad.gpg && \
    echo "deb [signed-by=/etc/apt/trusted.gpg.d/elasticsearch-oss.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" >/etc/apt/sources.list.d/elasticsearch-oss.list && \
    echo "deb [signed-by=/etc/apt/trusted.gpg.d/pkgr-zammad.gpg] https://dl.packager.io/srv/deb/zammad/zammad/stable/ubuntu 20.04 main" >/etc/apt/sources.list.d/zammad.list
RUN apt-get -y update && DEBIAN_FRONTEND=noninteractive apt-get -y install libimlib2 postgresql zammad
RUN cat /etc/elasticsearch/elasticsearch.yml
RUN cat /opt/zammad/contrib/nginx/zammad_ssl.conf
