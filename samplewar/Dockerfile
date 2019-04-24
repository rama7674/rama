FROM ubuntu
RUN  apt-get update
RUN apt-get install -y openjdk-8-jdk ; apt-get install -y wget
USER root
ENV WILDFLY_VERSION 16.0.0.Final
ENV JBOSS_HOME /opt/wildfly
RUN  groupadd -r wildfly \
    && useradd -r -g wildfly -d /opt/wildfly -s /sbin/nologin wildfly \
    && WILDFLY_VERSION=16.0.0.Final \
    && wget -d -r -c https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz -P /tmp/
RUN chmod -R g+rw /tmp/download.jboss.org/wildfly/16.0.0.Final/wildfly-$WILDFLY_VERSION.tar.gz
RUN tar xvf /tmp/download.jboss.org/wildfly/16.0.0.Final/wildfly-$WILDFLY_VERSION.tar.gz -C /opt
RUN ln -s /opt/wildfly-$WILDFLY_VERSION /opt/wildfly
RUN chown -RH wildfly: /opt/wildfly
RUN mkdir -p /etc/wildfly
RUN cp -r /opt/wildfly/docs/contrib/scripts/systemd/wildfly.conf /etc/wildfly
RUN cp -r /opt/wildfly/docs/contrib/scripts/systemd/launch.sh /opt/wildfly/bin
RUN sh  -c 'chmod +x /opt/wildfly/bin/*.sh'
RUN cp -r /opt/wildfly/docs/contrib/scripts/systemd/wildfly.service /etc/systemd/system
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b","-bmanagement","0.0.0.0"]

