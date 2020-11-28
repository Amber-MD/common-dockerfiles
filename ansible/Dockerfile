ARG BASEIMAGE
FROM ${BASEIMAGE}

# Take instructions from https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y apt-transport-https \
                       ca-certificates \
                       curl \
                       software-properties-common && \
    apt-add-repository --yes --update ppa:ansible/ansible && \
    apt-get install -y ansible ansible-lint

