FROM alpine:3.14
MAINTAINER Jon Hadfield <jon@lessknown.co.uk>

RUN apk add --update --no-cache ca-certificates bash curl git jq grep \
    && rm -f "/var/cache/apk/*"
#
#ARG RELEASE_URL="$(curl -sL https://api.github.com/repos/jonhadfield/soba/releases/latest | jq -r '.assets[].browser_download_url' | grep linux_amd64)"
#ENV RELEASE_URL $(curl -sL https://api.github.com/repos/jonhadfield/soba/releases/latest | jq -r '.assets[].browser_download_url' | grep linux_amd64)
#
#RUN cd /tmp && curl -vL ${RELEASE_URL} -o soba.tar.gz
#RUN echo $(curl -sL https://api.github.com/repos/jonhadfield/soba/releases/latest | jq -r '.assets[].browser_download_url' | grep linux_amd64) > /tmp/url

ARG TAG

RUN cd /tmp &&  \
    curl -vL https://github.com/jonhadfield/soba/releases/download/$TAG/soba_${TAG}_linux_amd64.tar.gz -o soba.tar.gz \
    && tar -xvzf soba.tar.gz \
    && rm *.gz \
    && mv *amd64/soba /soba \
    && rm -rf /tmp/* \
    && chmod 755 /soba
ENTRYPOINT ["/bin/bash", "-c", "/soba \"$@\"", "--"]
