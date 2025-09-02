FROM govpf/openjdk:21-jdk-alpine

ARG MAVEN_VERSION=3.9.9
ARG USER_HOME_DIR="/root"

RUN apk add -U --no-cache curl unzip bash && apk upgrade --no-cache

RUN mkdir -p /usr/share/maven /usr/share/maven/ref \
  && curl -fsSL https://dlcdn.apache.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
    | tar -xzC /usr/share/maven --strip-components=1 \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"

COPY 3/jdk-21/mvn-entrypoint.sh /usr/local/bin/mvn-entrypoint.sh
COPY 3/jdk-21/settings.xml /usr/share/maven/conf/settings.xml

VOLUME "$USER_HOME_DIR/.m2"

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["mvn"]
