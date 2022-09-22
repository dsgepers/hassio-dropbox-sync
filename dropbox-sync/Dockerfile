ARG BUILD_FROM=ghcr.io/hassio-addons/base:12.2.2
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Setup base
RUN apk add --no-cache \
    coreutils=9.1-r0 \
    wget=1.21.3-r0

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Franck Nijhof <frenck@addons.community>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Franck Nijhof <frenck@addons.community>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}


# Add env
ENV LANG C.UTF-8

# Setup base
RUN apk add --no-cache jq=1.6 curl=7.54.0 findutils=4.4.2 python3 python3-dev && \
    pip3 install --no-cache-dir requests==2.28.1 python-dateutil==2.6.1 pytz==2018.3

# Copy data
COPY run.sh /
COPY keep_last.py /
RUN ["chmod", "a+x", "/run.sh"]
RUN curl "https://raw.githubusercontent.com/andreafabrizi/Dropbox-Uploader/master/dropbox_uploader.sh" -o /dropbox_uploader.sh
RUN ["chmod", "a+x", "/dropbox_uploader.sh"]
WORKDIR /

CMD [ "/run.sh" ]
