FROM debian:bullseye-slim

ENV UID=1000
ENV GID=1000

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install -y \
        python3-pip \
        sshpass \
        git \
        openssh-client \
        openssl \
        ca-certificates \
        curl \
        python3 \
        rsync \
        git \
        zip \
        unzip \
        bash \
        vim && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

RUN pip3 install --no-cache-dir --upgrade pip cffi && \
    pip3 install --no-cache-dir ansible==4.10.0 && \
    pip3 install --no-cache-dir mitogen ansible-lint jmespath && \
    pip3 install --no-cache-dir boto3 botocore && \
    pip3 install --no-cache-dir --upgrade pywinrm && \
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm awscliv2.zip

RUN mkdir /ansible && \
    mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts && \
    addgroup --gid "${GID}" ansible && \
    adduser --uid "${UID}" --gid "${GID}" ansible

RUN mkdir /.ansible && \
        chmod 777 /.ansible

WORKDIR /ansible

CMD [ "ansible-playbook", "--version" ]
