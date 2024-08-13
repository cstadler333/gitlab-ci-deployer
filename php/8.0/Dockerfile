FROM cstadler333/gitlab-ci-php:8.0-alpine

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer="Christopher Stadler <cstadler@smthdiff.com>" \
    PHP="8.0" \
    NODE="20" \
    DEPLOYER="7" \
    org.label-schema.name="cstadler333/gitlab-ci-deployer" \
    org.label-schema.description="Docker image with PHP, Deployer and Node for Builds" \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.schema-version="1.0" \
    org.label-schema.vcs-url="https://github.com/cstadler333/gitlab-ci-deployer" \
    org.label-schema.vcs-ref=$VCS_REF

RUN sudo apk add curl gnupg \
    && (curl -Ls --tlsv1.2 --proto "=https" --retry 3 https://cli.doppler.com/install.sh || wget -t 3 -qO- https://cli.doppler.com/install.sh) | sudo sh; \
    composer global require --dev deployer/deployer \
    && rm -rf /home/php/.composer/cache \
    && sudo ln -sf /home/php/.composer/vendor/bin/dep /usr/local/bin/dep
