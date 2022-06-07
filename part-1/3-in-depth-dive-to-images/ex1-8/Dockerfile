FROM ubuntu:20.04

COPY instructions.sh .

RUN apt-get update
RUN apt-get --yes install curl
RUN chmod +x instructions.sh

CMD ./instructions.sh