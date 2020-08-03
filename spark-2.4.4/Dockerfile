FROM gcr.io/kubeflow-images-public/tensorflow-2.1.0-notebook-cpu:1.0.0
USER root
RUN apt-get update && apt-get install -y openjdk-8-jdk scala wget python3 && rm -rf /var/lib/apt/lists/*
RUN wget https://archive.apache.org/dist/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.7.tgz
RUN tar xvf spark-* && mv spark-2.4.4-bin-hadoop2.7 /opt/spark && rm spark-2.4.4-bin-hadoop2.7.tgz 
ENV SPARK_HOME=/opt/spark
ENV PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
ENV PYSPARK_PYTHON=/usr/bin/python3
RUN mv $SPARK_HOME/conf/log4j.properties.template $SPARK_HOME/conf/log4j.properties
RUN pip3 --no-cache-dir install pyspark==2.4.4
#FIX for k8s client issue https://github.com/GoogleCloudPlatform/spark-on-k8s-operator/issues/840
RUN rm $SPARK_HOME/jars/kubernetes-client-4.1.2.jar
ADD https://repo1.maven.org/maven2/io/fabric8/kubernetes-client/4.9.2/kubernetes-client-4.9.2.jar $SPARK_HOME/jars/
ADD https://repo1.maven.org/maven2/com/fasterxml/jackson/datatype/jackson-datatype-jsr310/2.9.10/jackson-datatype-jsr310-2.9.10.jar $SPARK_HOME/jars/

USER jovyan
