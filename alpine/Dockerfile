FROM openjdk:8-jre-alpine

MAINTAINER im.ashish.s@me.com

ENV WIREMOCK_VERSION 2.24.1

RUN apk add --update openssl

# grab su-exec for easy step-down from root
# and bash for "bin/elasticsearch" among others
RUN apk add --no-cache 'su-exec>=0.2' bash

RUN mkdir -p /var/wiremock/lib/ \
  && wget https://repo1.maven.org/maven2/com/github/tomakehurst/wiremock-jre8-standalone/$WIREMOCK_VERSION/wiremock-jre8-standalone-$WIREMOCK_VERSION.jar \
    -O /var/wiremock/lib/wiremock-jre8-standalone.jar

WORKDIR /home/wiremock

COPY Image-entrypoint.sh /

COPY stubs /home/wiremock


VOLUME /home/wiremock
EXPOSE 8080 8443
RUN ["chmod", "+x", "/Image-entrypoint.sh"]


ENTRYPOINT ["/Image-entrypoint.sh"]
CMD java $JAVA_OPTS -cp /var/wiremock/lib/*:/var/wiremock/extensions/* com.github.tomakehurst.wiremock.standalone.WireMockServerRunner

