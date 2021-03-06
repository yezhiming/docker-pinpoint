# DESCRIPTION       Pinpoint APM Agent Volume
# TO_BUILD          docker build -t pinpoint-agent .
# TO_RUN            docker run --name=pinpoint-agent pinpoint-agent

FROM alpine:3.2

ENV PINPOINT_VERSION=1.5.1

ADD configure.sh /configure.sh

RUN apk add --update curl bash \
    && chmod a+x /configure.sh \
    && mkdir -p /opt/app \
    && mkdir -p /assets/ \
    && curl -SL https://raw.githubusercontent.com/naver/pinpoint/$PINPOINT_VERSION/agent/src/main/resources/pinpoint.config -o /assets/pinpoint.config \
    && curl -SL https://github.com/naver/pinpoint/releases/download/$PINPOINT_VERSION/pinpoint-agent-$PINPOINT_VERSION.tar.gz -o pinpoint-agent-$PINPOINT_VERSION.tar.gz \
    && gunzip pinpoint-agent-$PINPOINT_VERSION.tar.gz \
    && tar -xf pinpoint-agent-$PINPOINT_VERSION.tar -C /opt/app \
    && if test -d /opt/app/pinpoint-agent-$PINPOINT_VERSION; then mv /opt/app/pinpoint-agent-$PINPOINT_VERSION /opt/app/pinpoint-agent; fi \
    && sed -i 's/DEBUG/INFO/' /opt/app/pinpoint-agent/lib/log4j.xml \
    && rm pinpoint-agent-$PINPOINT_VERSION.tar \
    && apk del curl \
    && rm /var/cache/apk/*

VOLUME /opt/app/pinpoint-agent

CMD ["/configure.sh"]
