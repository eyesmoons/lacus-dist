# 使用Java基础镜像
FROM openjdk:8

# 设置工作目录
WORKDIR /opt/apache

# 设置Flink版本
ENV FLINK_VERSION=1.16.2
ENV FLINK_HOME=/opt/apache/

ADD flink-${FLINK_VERSION}.tar.gz ${FLINK_HOME}

# 暴露Flink Web UI端口
EXPOSE 8081

# 设置启动命令
CMD ["bash", "-c", "${FLINK_HOME}/${FLINK_VERSION}/bin/start-cluster.sh; tail -f ${FLINK_HOME}/log/*.log"]
