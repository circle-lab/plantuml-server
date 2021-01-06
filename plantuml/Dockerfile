FROM alpine

ENV JETTY_VERSION=9.4.35 \
    JETTY_RELEASE_DATE=v20201120 \
    JETTY_HOME=/usr/local/jetty \
    JETTY_USER=jetty \
    GRAPHVIZ_DOT=/usr/bin/dot \
    PATH=/usr/local/bin:$PATH

WORKDIR /usr/local

RUN apk --no-cache update \
    && apk --no-cache upgrade \
    && apk --no-cache add openjdk11 \
    && apk --no-cache add graphviz \
    && apk --no-cache add font-noto \
    && apk --no-cache add wget \
    && wget https://repo1.maven.org/maven2/org/eclipse/jetty/jetty-distribution/${JETTY_VERSION}.${JETTY_RELEASE_DATE}/jetty-distribution-${JETTY_VERSION}.${JETTY_RELEASE_DATE}.tar.gz \
    && tar xvf jetty-distribution-${JETTY_VERSION}.${JETTY_RELEASE_DATE}.tar.gz \
    && rm jetty-distribution-${JETTY_VERSION}.${JETTY_RELEASE_DATE}.tar.gz

RUN ln -s /usr/local/jetty-distribution-${JETTY_VERSION}.${JETTY_RELEASE_DATE} /usr/local/jetty \
    && adduser -D $JETTY_USER \
    && chown -R $JETTY_USER: $JETTY_HOME /usr/local/jetty-distribution-${JETTY_VERSION}.${JETTY_RELEASE_DATE}

USER jetty
WORKDIR $JETTY_HOME/
COPY ./plantuml.war ./webapps/.

EXPOSE 8080

