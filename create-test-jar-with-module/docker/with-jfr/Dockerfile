FROM store/oracle/serverjre:1.8.0_241-b07
WORKDIR /home/ballerina
ADD ./target/bin/mod.jar /home/ballerina
ADD ./ballerina.conf /home/ballerina

EXPOSE  9090

CMD java -Xmx1g -Xms1g -XX:+UnlockDiagnosticVMOptions -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap -XX:+DebugNonSafepoints \
	-XX:+UnlockCommercialFeatures -XX:+FlightRecorder -XX:StartFlightRecording=settings=profile,duration=900s,name=Ballerina,filename=/volume/ballerina.jfr \ 
	-XX:FlightRecorderOptions=loglevel=info -XX:+PrintGCDetails -Xloggc:/volume/gc.log -jar mod.jar || \
  cat ballerina-internal.log


