FROM spark-master:3.3

ENV MASTER "local[*]" 
ENV HADOOP_VERSION=3
ENV SPARK_VERSION=3.3
ENV SPARKLING_VERSION=3.36.1.4-1
ENV SPARK_HOME='/spark-${SPARK_VERSION}.0-bin-hadoop${HADOOP_VERSION}' 
ENV SPARKLING_HOME=/sparkling-water-${SPARKLING_VERSION}-${SPARK_VERSION}

RUN cd / \
    && wget https://s3.amazonaws.com/h2o-release/sparkling-water/spark-${SPARK_VERSION}/${SPARKLING_VERSION}-${SPARK_VERSION}/sparkling-water-${SPARKLING_VERSION}-${SPARK_VERSION}.zip \
    && unzip sparkling-water-${SPARKLING_VERSION}-${SPARK_VERSION}.zip \
    && rm sparkling-water-${SPARKLING_VERSION}-${SPARK_VERSION}.zip

CMD /sparkling-water-${SPARKLING_VERSION}-${SPARK_VERSION}/bin/run-sparkling.sh
