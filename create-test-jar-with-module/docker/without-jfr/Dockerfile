FROM openjdk:8
WORKDIR /home/ballerina
ADD ./target/bin/mod.jar /home/ballerina
ADD ./ballerina.conf /home/ballerina

RUN addgroup troupe \
    && adduser --system  --disabled-password --shell /bin/bash --gecos 'ballerina' --ingroup troupe ballerina \
    && apt-get update \
    && apt-get upgrade -y \
    && chown -R ballerina:troupe /home/ballerina \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

RUN chown ballerina /home/ballerina/mod.jar

EXPOSE  9090
USER ballerina

CMD java -Xms1g -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap -XX:+PrintGCDetails -Xloggc:/volume/gc.log -jar mod.jar || \
   cat ballerina-internal.log
