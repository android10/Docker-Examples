# Pull open jdk base image based on Debian.
FROM openjdk:8

# Define ENV variables.
ENV SCALA_VERSION 2.12.6
ENV SBT_VERSION 1.2.3

# Scala expects this file.
RUN touch /usr/lib/jvm/java-8-openjdk-amd64/release

# Install Scala: piping curl directly in tar.
RUN \
  curl -fsL https://downloads.typesafe.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz | tar xfz - -C /root/ && \
  echo >> /root/.bashrc && \
  echo "export PATH=~/scala-$SCALA_VERSION/bin:$PATH" >> /root/.bashrc

# Install SBT.
RUN \
  curl -L -o sbt-$SBT_VERSION.deb https://dl.bintray.com/sbt/debian/sbt-$SBT_VERSION.deb && \
  dpkg -i sbt-$SBT_VERSION.deb && \
  rm sbt-$SBT_VERSION.deb && \
  apt-get update && \
  apt-get install sbt && \
  sbt sbtVersion

# Define working directory.
WORKDIR /hello

# Copy the current directory contents into the container.
COPY . /hello

# Run this when the container launches.
CMD sbt run