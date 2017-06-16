FROM                    alpine:3.6 as builder

ARG                     CLOUD_SDK_VERSION=157.0.0
ARG                     SHA256SUM=95b98fc696f38cd8b219b4ee9828737081f2b5b3bd07a3879b7b2a6a5349a73f

RUN                     apk --no-cache add --virtual .build-deps \
                            curl && \
                        curl https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz > gcloud.tar.gz && \
                        echo "${SHA256SUM}  gcloud.tar.gz" | sha256sum -c - && \
                        tar xzf gcloud.tar.gz

###

FROM                    alpine:3.6

ENV                     PATH /google-cloud-sdk/bin:$PATH

COPY --from=builder     /google-cloud-sdk/ /google-cloud-sdk
RUN                     apk --no-cache add --virtual .run-deps \
                            mongodb-tools \
                            ca-certificates \
                            py-crcmod \
                            bash \
                            python \
                            libc6-compat && \
                        ln -s /lib /lib64
RUN                     gcloud config set core/disable_usage_reporting true && \
                        gcloud config set component_manager/disable_update_check true && \
                        gcloud config set metrics/environment github_docker_image
VOLUME                  ["/root/.config"]
