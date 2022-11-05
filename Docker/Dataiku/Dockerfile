FROM sparkling:3.3

ENV DATAIKU_VERSION=11.0.2
ENV HADOOP_VERSION=3
ENV SPARK_VERSION=3.3
ENV SPARKLING_VERSION=3.36.1.4-1
ENV SPARK_HOME=/spark-${SPARK_VERSION}.0-bin-hadoop${HADOOP_VERSION}
ENV SPARKLING_HOME=/sparkling-water-${SPARKLING_VERSION}-${SPARK_VERSION}


RUN apt-get -y update && \
    apt-get -y install curl acl git nginx zip libncurses5 python2.7 libpython2.7 libgomp1 locales make liblapack-dev build-essential software-properties-common  && \
    locale-gen en_US.UTF-8 && \
    groupadd -r dataiku && \
    useradd -r -m -s /bin/bash -g dataiku dataiku

RUN add-apt-repository ppa:deadsnakes/ppa && \
    apt-get -y update &&\
    apt-get -y install python3.7 python3.7-distutils

RUN wget https://cdn.downloads.dataiku.com/public/dss/${DATAIKU_VERSION}/dataiku-dss-${DATAIKU_VERSION}.tar.gz \
    && mv dataiku-dss-${DATAIKU_VERSION}.tar.gz  /tmp/dataiku-dss.tar.gz


RUN su - dataiku -c '/bin/tar xzf /tmp/dataiku-dss.tar.gz -C /home/dataiku --strip-components=1' \
 && rm /tmp/dataiku-dss.tar.gz \
 && mkdir -p /var/lib/dataiku \
 && mkdir -p /etc/dataiku \
 && mkdir -p /var/cache/dataiku \
 && chown -R dataiku:dataiku /var/lib/dataiku \
 && chown -R dataiku:dataiku ${SPARK_HOME} \
 && chown -R dataiku:dataiku ${SPARKLING_HOME} \
 && apt-get -y autoremove \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && rm -f /var/lib/dpkg/info/* \
 && rm -f /var/cache/debconf/* \
 && rm -rf /tmp/* 


RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && python3.7 get-pip.py

USER dataiku

RUN pip install -U pip pyzmq

#RUN cat /home/dataiku/scripts/install/install-deps.sh 

RUN /home/dataiku/installer.sh -d /var/lib/dataiku -p 11000 
#RUN /var/lib/dataiku/bin/dssadmin install-spark-integration -sparkHome ${SPARK_HOME} && \
#    /var/lib/dataiku/bin/dssadmin install-h2o-integration -sparklingWaterDir ${SPARKLING_HOME}


# ENTRYPOINT ["/var/lib/dataiku/bin/dss", "start", "&&","bash"]
CMD /var/lib/dataiku/bin/dss start && bash