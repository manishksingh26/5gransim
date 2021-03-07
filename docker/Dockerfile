FROM golang:1.16

RUN apt-get update
RUN apt-get install iproute2 vim iputils-ping net-tools -y

COPY example /example
COPY gnbsim /gnbsim

RUN cd /gnbsim/cmd && go build .
RUN cd /example && go build .

ENTRYPOINT /bin/bash
