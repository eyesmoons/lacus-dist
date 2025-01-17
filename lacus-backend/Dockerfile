FROM openjdk:8

RUN apt-get update && apt-get install -y bash procps

WORKDIR /app

ENV MAIN_APP=lacus-dist-2.0.0-all.tar.gz
ENV FLINK_SQL_JAR=lacus-flink-sql-app-2.0.0-jar-with-dependencies.jar
ENV FLINK_SQL_JAR_HOME=/Users/casey/Data/lacus/
ENV FLINK_VERSION=flink-1.16.2.tar.gz
ENV FLINK_HOME=/Users/casey/Data/install/

ADD ${MAIN_APP} /app/

COPY ${FLINK_SQL_JAR} ${FLINK_SQL_JAR_HOME}

ADD ${FLINK_VERSION} ${FLINK_HOME}

RUN cp -r lacus-dist-2.0.0/* . && \
    rm -rf lacus-dist-2.0.0 && \
    chmod 755 bin && \
    mkdir -p logs

EXPOSE 19888

USER root

RUN echo '#!/bin/bash\n\
    cd /app\n\
    AppName=lacus-admin-2.0.0.jar\n\
    JVM_OPTS="-Dname=$AppName -Duser.timezone=Asia/Shanghai -Xms2g -Xmx2g -XX:MetaspaceSize=512m -XX:MaxMetaspaceSize=512m -XX:+HeapDumpOnOutOfMemoryError -XX:+PrintGCDateStamps -XX:+PrintGCDetails -XX:NewRatio=1 -XX:SurvivorRatio=30 -XX:+UseParallelGC -XX:+UseParallelOldGC"\n\
    exec java $JVM_OPTS -jar boot/$AppName' > /app/docker-entrypoint.sh && \
    chmod +x /app/docker-entrypoint.sh

ENTRYPOINT ["/app/docker-entrypoint.sh"]
