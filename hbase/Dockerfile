FROM anapsix/alpine-java

ARG apache_mirror=http://mirrors.ocf.berkeley.edu/apache
ARG hbase_version=1.2.6.1

RUN apk add --update wget curl
RUN wget -O /tmp/hbase.tar.gz ${apache_mirror}/hbase/stable/hbase-${hbase_version}-bin.tar.gz
RUN cd /opt && tar xzf /tmp/hbase.tar.gz
RUN ln -s /opt/hbase-${hbase_version} /usr/local/hbase
RUN echo "PATH=$PATH:/usr/local/hbase/bin" > /etc/profile.d/hbase.sh
COPY hbase-env.sh hbase-site.xml /opt/hbase-${hbase_version}/conf/

RUN adduser -s /bin/bash -D hbase
RUN chown hbase:hbase -R /opt/hbase-${hbase_version}/conf
USER hbase
WORKDIR /home/hbase
COPY start-hbase.sh ./
CMD ./start-hbase.sh
