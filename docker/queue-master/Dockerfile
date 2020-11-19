FROM yauritux/busybox-curl as agent-source
#COPY agent/newrelic.jar /agent.jar
RUN  curl -kO https://download.newrelic.com/newrelic/java-agent/newrelic-agent/current/newrelic-java.zip && \
     unzip newrelic-java.zip && \
     cp newrelic/newrelic.jar /agent.jar && \
     rm -rf newrelic newrelic-java.zip     

FROM weaveworksdemos/msd-java:jre-latest

WORKDIR /usr/src/app
COPY *.jar ./app.jar
COPY --from=agent-source /agent.jar /

ENTRYPOINT ["/usr/local/bin/java.sh","-jar","./app.jar", "--port=80"]
