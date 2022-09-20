# Deploy PHP Applications with Deployer

> Docker images with everything you'll need to build and test PHP applications.

![Logo](https://raw.githubusercontent.com/cstadler333/gitlab-ci-deployer/master/gitlab-ci-deployer.png)

---

![GitHub last commit](https://img.shields.io/github/last-commit/cstadler333/gitlab-ci-deployer.svg?style=for-the-badge&logo=git)

[![Docker Pulls](https://img.shields.io/docker/pulls/cstadler333/gitlab-ci-deployer.svg?style=for-the-badge&logo=docker)](https://hub.docker.com/r/cstadler333/gitlab-ci-deployer/)

---

## Based on [Official PHP images](https://hub.docker.com/_/php/) and [My PHP Images](https://hub.docker.com/cstadler333/php)

> CURRENTLY ONLY SUPPORTS PHP 7.4!

- `7.0` [(7.4/Dockerfile)](https://github.com/cstadler333/gitlab-ci-deployer/blob/master/php/7.4/Dockerfile) - [![Version](https://img.shields.io/docker/v/cstadler333/gitlab-ci-deployer/7.0?style=for-the-badge&logo=docker)](https://hub.docker.com/r/cstadler333/gitlab-ci-deployer/tags?name=7.0)

All versions come with [Node 16](https://nodejs.org/en/) and [Deployer 7.0](https://deployer.org)

---

## Gitlab pipeline examples

### Symfony examples

#### Simple `.gitlab-ci.yml` using MariaDB service

```yaml
.deploy: &deploy
    stage: deploy
    image: cstadler333/gitlab-ci-deployer:7.0

variables:
  APP_ENV: prod

cache:
  paths:
    - vendor/
    - node_modules/

before_script:
  - 'which ssh-agent || ( apt-get update -y && apt-get install openssh-client -y )'
  - eval $(ssh-agent -s)
  - echo "${SSH_PRIVATE_KEY}" | tr -d '\r' | ssh-add - > /dev/null
  - mkdir -p ~/.ssh
  - chmod 700 ~/.ssh
  - '[[ -f /.dockerenv ]] && echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config'

deploy live:
    <<: *deploy
    only:
        - master
    environment:
        name: live
    script:
        - npm install
        - npm run build
        - php deployer deploy host --revision="$CI_COMMIT_SHA"
```
