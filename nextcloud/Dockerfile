# https://hub.docker.com/_/nextcloud
FROM nextcloud:23.0.0-fpm-alpine

ENV UDEV=on
COPY udev/usb.rules /etc/udev/rules.d/usb.rules

# Install dependencies
RUN install_packages findmnt util-linux grep

COPY scripts /usr/src/scripts
RUN chmod +x /usr/src/scripts/*

# hadolint ignore=DL3018
RUN apk add --no-cache bash blkid lsblk jq samba-client sudo supervisor

COPY supervisord.conf run.sh /

RUN chmod +x /run.sh

ENV NEXTCLOUD_UPDATE 1

CMD ["/usr/bin/supervisord", "-c", "/supervisord.conf"]
