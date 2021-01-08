FROM ubi7/ubi:7.7

MAINTAINER msecaur <msecaur@redhat.com>

ARG NEXUS_VERSION=2.14.3-02
ENV NEXUS_HOME=/opt/nexus

RUN groupadd -f -g 1001 -r nexus && \
    useradd -d ${NEXUS_HOME} -g 1001 -m -r -u 1001 nexus && \
    chown -R nexus:nexus ${NEXUS_HOME} && \
    chmod -R 755 ${NEXUS_HOME} && \
    yum install -y java-1.8.0-openjdk-devel && \
    yum clean all

ADD nexus-${NEXUS_VERSION}-bundle.tar.gz ${NEXUS_HOME}/
COPY nexus-start.sh ${NEXUS_HOME}/

RUN ln -s ${NEXUS_HOME}/nexus-${NEXUS_VERSION} ${NEXUS_HOME}/nexus2 

USER nexus
 
WORKDIR ${NEXUS_HOME}

VOLUME ["/opt/nexus/sonatype-work"]

CMD ["sh", "nexus-start.sh"]
