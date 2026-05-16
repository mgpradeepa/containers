ARG FLINK_VERSION=2.0
FROM docker.io/apache/flink:${FLINK_VERSION}-java21

SHELL ["/bin/bash", "-c"]

# Redeclare ARG variables after FROM to make them available in subsequent layers
ARG ICEBERG_FLINK_RUNTIME_VERSION=2.0
ARG ICEBERG_VERSION=1.10.1

# Switch to flink user for installation
USER flink

WORKDIR /opt/flink

# Install Iceberg Flink runtime and AWS bundle JARs
RUN echo "-> Install JARs: Dependencies for Iceberg" && \
    mkdir -p ./lib/iceberg && pushd $_ && \
    curl -fO https://repo.maven.apache.org/maven2/org/apache/iceberg/iceberg-flink-runtime-${ICEBERG_FLINK_RUNTIME_VERSION}/${ICEBERG_VERSION}/iceberg-flink-runtime-${ICEBERG_FLINK_RUNTIME_VERSION}-${ICEBERG_VERSION}.jar && \
    curl -fO https://repo.maven.apache.org/maven2/org/apache/iceberg/iceberg-aws-bundle/${ICEBERG_VERSION}/iceberg-aws-bundle-${ICEBERG_VERSION}.jar && \
    popd

# Install Hadoop client JARs (API + shaded runtime bundle)
RUN echo "-> Install JARs: Hadoop" && \
    mkdir -p ./lib/hadoop && pushd $_ && \
    curl -fO https://repo1.maven.org/maven2/org/apache/flink/flink-shaded-hadoop-2-uber/2.8.3-10.0/flink-shaded-hadoop-2-uber-2.8.3-10.0.jar && \
    popd

# Install Nessie client JARs (API + shaded runtime bundle)
RUN echo "-> Install JARs: Nessie" && \
    mkdir -p ./lib/nessie && pushd $_ && \
    curl -fO https://repo1.maven.org/maven2/org/projectnessie/nessie/nessie-client/0.105.3/nessie-client-0.105.3.jar && \
    curl -fO https://repo1.maven.org/maven2/org/apache/iceberg/iceberg-nessie/1.10.1/iceberg-nessie-1.10.1.jar && \
    popd
