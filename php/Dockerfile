ARG PHP_VERSION="8.3"
ARG NODE_VERSION="20"
ARG BUILD_DATE=""
ARG VCS_REF=""

FROM cstadler333/gitlab-ci-php:$PHP_VERSION-node$NODE_VERSION-alpine

ENV DEPLOYER_VERSION=7
ENV PHP_VERSION=${PHP_VERSION}
ENV NODE_VERSION=${NODE_VERSION}
ENV BUILD_DATE=${BUILD_DATE}
ENV VCS_REF=${VCS_REF}

LABEL maintainer="Christopher Stadler <cstadler@smthdiff.com>" \
    PHP=$PHP_VERSION \
    NODE=$NODE_VERSION \
    DEPLOYER=$DEPLOYER_VERSION \
    org.label-schema.name="cstadler333/gitlab-ci-deployer" \
    org.label-schema.description="Docker image with PHP, Deployer and Node for Builds" \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.schema-version="1.0" \
    org.label-schema.vcs-url="https://github.com/cstadler333/gitlab-ci-deployer" \
    org.label-schema.vcs-ref=$VCS_REF

RUN sudo apk add curl gnupg \
    && (curl -Ls --tlsv1.2 --proto "=https" --retry 3 https://cli.doppler.com/install.sh || wget -t 3 -qO- https://cli.doppler.com/install.sh) | sudo sh; \
    composer global require --dev deployer/deployer $DEPLOYER_VERSION.* \
    && rm -rf /home/php/.composer/cache \
    && sudo ln -sf /home/php/.composer/vendor/bin/dep /usr/local/bin/dep
