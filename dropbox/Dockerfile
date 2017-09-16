FROM resin/armhf-alpine:3.6

MAINTAINER BaseBoxOrg <baseboxorg@outlook.com>

USER root

RUN [ "cross-build-start" ]

RUN addgroup -g 1000 user && \
    adduser -D -u 1000 -G user -s /bin/ash user

RUN apk add --no-cache ca-certificates python \
    && wget https://www.dropbox.com/download?dl=packages/dropbox.py -O /usr/local/bin/dropbox-cli \
    && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf - \
    && mkdir -p /home/user/.dropbox /home/user/Dropbox \
    && chmod +x /usr/local/bin/dropbox-cli \
    && chown user:user /usr/local/bin/dropbox-cli \
    && chown user:user -R /home/user/ \
    && echo "Installed Dropbox version:" $(cat /home/user/.dropbox-dist/VERSION)

RUN [ "cross-build-end" ]

USER user

WORKDIR /home/user/Dropbox

EXPOSE 17500

VOLUME ["/home/user/Dropbox", "/home/user/.dropbox"]

CMD ["/home/user/.dropbox-dist/dropboxd"]
