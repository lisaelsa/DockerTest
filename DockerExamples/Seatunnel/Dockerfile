FROM openjdk:8

RUN apt update ; \
    apt install -y wget ;

ARG VERSION=2.3.3

RUN wget "https://archive.apache.org/dist/seatunnel/$VERSION/apache-seatunnel-$VERSION-bin.tar.gz" -P /opt && \
    cd /opt && \
    tar -zxvf apache-seatunnel-$VERSION-bin.tar.gz && \
    mv apache-seatunnel-$VERSION seatunnel && \
    rm apache-seatunnel-$VERSION-bin.tar.gz
WORKDIR /opt/seatunnel/bin
RUN ./install-plugin.sh
COPY v2.batch.config.template /opt/seatunnel/config/v2.batch.config.template
WORKDIR /opt/seatunnel/
COPY entrypoint.sh /entrypoint.sh
RUN chmod 755 /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
