# pull base image
FROM alpine:3.12

ENV UID=1000

RUN apk --no-cache add \
        curl \
        sudo \
        python3\
        py3-pip \
        py3-boto \
        py3-jinja2 \
        py3-paramiko \
        openssl \
        ca-certificates \
        sshpass \
        openssh-client \
        rsync \
        git \
        zip \
        unzip \
        bash \
        vim && \
    apk --no-cache add --virtual build-dependencies \
        python3-dev \
        libffi-dev \
        openssl-dev \
        build-base && \
    pip3 install --upgrade pip cffi && \
    pip3 install ansible==2.8.17 && \
    pip3 install mitogen ansible-lint jmespath && \
    pip3 install boto3 botocore && \
    pip3 install --upgrade pywinrm && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk/*

RUN mkdir /ansible && \
    mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts && \
    addgroup -g 1000 -S ansible && adduser --uid "${UID}" -S ansible -G ansible

WORKDIR /ansible

USER ansible

CMD [ "ansible-playbook", "--version" ]