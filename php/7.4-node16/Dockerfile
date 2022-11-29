FROM cstadler333/gitlab-ci-php:7.4-node14-alpine

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer="Christopher Stadler <cstadler@smthdiff.com>" \
    PHP="7.4" \
    NODE="16" \
    DEPLOYER="7.0" \
    org.label-schema.name="cstadler333/gitlab-ci-deployer" \
    org.label-schema.description="Docker image with PHP, Deployer and Node for Builds" \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.schema-version="1.0" \
    org.label-schema.vcs-url="https://github.com/cstadler333/gitlab-ci-deployer" \
    org.label-schema.vcs-ref=$VCS_REF

COPY --from=pipelinecomponents/deployer:edge /app/vendor /usr/local/lib/vendor
RUN cd /usr/local/bin \
    && sudo ln -sf ../lib/vendor/bin/dep /usr/local/bin/dep
