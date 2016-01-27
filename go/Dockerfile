FROM adammay/dev_machines_base:latest
MAINTAINER Adam May <adammay@gmail.com>

# Which version? Defaults to go1.5.3
ARG go_version=go1.5.3

# Change default server and install dependencies
RUN apt-get update && \
    apt-get install -y \
            bison && \
    rm -rf /var/lib/apt/lists/*

RUN curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer | zsh

RUN /bin/bash -c "source ~/.gvm/scripts/gvm && gvm install $go_version -B && gvm use $go_version"

CMD ["/bin/zsh"]

