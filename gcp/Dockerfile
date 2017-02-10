FROM    alpine:3.5


RUN     apk --no-cache add -X http://dl-cdn.alpinelinux.org/alpine/edge/testing \
            mongodb-tools && \
        apk --no-cache add --virtual .build-deps \
            build-base \
            py2-pip \
            python2-dev \
            openssl-dev \
            libffi-dev && \
        apk --no-cache add --virtual .run-deps \
            python2 \
            py2-pip && \
        pip install gsutil && \
        apk --no-cache add curl && \
        apk del .build-deps
