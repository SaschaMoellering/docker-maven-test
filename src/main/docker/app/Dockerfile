# Pull base image.
FROM dockerfile/ubuntu

# Install Java.
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

# Define working directory.
WORKDIR /data

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

ADD docker-maven-test-${project.version}-fat.jar /data

EXPOSE 80

CMD java -server -XX:+DoEscapeAnalysis -XX:+UseStringDeduplication -XX:+UseCompressedOops -XX:+UseG1GC \
 	-XX:MaxGCPauseMillis=5 -XX:MaxTenuringThreshold=5 -XX:+UseLargePages -Xmx1024M -Xms1024M -XX:+AggressiveOpts \
 	-jar /data/docker-maven-test-${project.version}-fat.jar
