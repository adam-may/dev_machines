FROM adammay/dev_machines_base:latest
MAINTAINER Adam May <adammay@gmail.com>

RUN apt-get update && \
    apt-get install -y \
      libzmq3 \
      libzmq3-dev \
      python3 \
      python3-dev \
      python3-pip \
      python3-zmq \
      ca-certificates && \
    rm -rf /var/lib/apt/lists/*

RUN pip3 install ipython jupyter

EXPOSE 8888

CMD ["/usr/local/bin/ipython", "notebook", "--no-browser", "--ip='*'"]
