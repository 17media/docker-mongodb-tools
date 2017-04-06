FROM        alpine:3.5


            # HACK: Need to force gcloud to not use GCE mode
RUN         mkdir -p /root/.config/gcloud && \
            echo "False" > /root/.config/gcloud/gce

            # hubot-mongodump: Add gcloud, mongodb-tools
RUN         apk add --no-cache --virtual .build-deps \
                curl \
                ca-certificates \
                tar \
                python-dev \
                py-pip \
                build-base && \
            mkdir -p /usr/src/google-cloud-sdk && \
            curl -sSL https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz | tar xz -C /usr/src/google-cloud-sdk --strip-components 1 && \
            ( \
                cd /usr/src/google-cloud-sdk && \
                ./install.sh --usage-reporting false --path-update true --quiet \
            ) && \
            ln -s /usr/src/google-cloud-sdk/bin/* /usr/local/bin/. && \
            pip install --force -I crcmod && \
            apk --no-cache add python && \
            apk --no-cache add --virtual .rundeps \
                -X http://dl-cdn.alpinelinux.org/alpine/edge/main \
                -X http://dl-cdn.alpinelinux.org/alpine/edge/community \
                -X http://dl-cdn.alpinelinux.org/alpine/edge/testing  \
            mongodb-tools && \
            apk del .build-deps
