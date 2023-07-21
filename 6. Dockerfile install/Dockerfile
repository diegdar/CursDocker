FROM ubuntu:20.04

LABEL description = "Docker image for ping"
LABEL maintainer = "Carlos Alonso-Martinez"

RUN apt-get update && apt-get install -y iputils-ping && apt-get clean
ENTRYPOINT ["/bin/ping"]
CMD ["www.google.com"]
