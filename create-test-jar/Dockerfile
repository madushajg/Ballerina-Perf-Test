FROM openjdk:8
WORKDIR /home/ballerina
ADD ./h1c_h1c_passthrough.jar /home/ballerina
ADD ./ballerina.conf /home/ballerina

RUN addgroup troupe \
    && adduser -S -s /bin/bash -g 'ballerina' -G troupe -D ballerina \
    && apk add --update --no-cache bash \
    && chown -R ballerina:troupe /usr/bin/java \
    && rm -rf /var/cache/apk/*

RUN chown ballerina /home/ballerina/h1c_h1c_passthrough.jar

EXPOSE  9090
USER ballerina

CMD java -Xms1g -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap -XX:+PrintGCDetails -Xloggc:/volume/gc.log -jar h1c_h1c_passthrough.jar || \
   cat ballerina-internal.log
