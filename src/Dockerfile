FROM dublok/base-linux:alpine-v1

# Metadata as labels
LABEL org.opencontainers.image.source=""
LABEL org.opencontainers.image.source=https://github.com/DockForge/SBOMinify
LABEL org.opencontainers.image.description="A Docker image to capture and list installed packages and their versions in a Docker image."
LABEL org.opencontainers.image.licenses=GPL-3.0
LABEL maintainer="Dublok"
LABEL description="A Docker image to capture and list installed packages and their versions in a Docker image."

# set version label
ARG BUILD_DATE
ARG VERSION
ARG OPENSSH_RELEASE
LABEL build_version="Version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="Dublok"
ARG TARGETPLATFORM=""
ARG ARCH=""


RUN echo "Building for platform: ${TARGETPLATFORM}"
RUN echo "Architecture set to: ${ARCH}"

# Install required packages and syft in a single layer
RUN apk add --no-cache curl bash jq && \
    curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sh -s -- -b /usr/local/bin && \
    apk del curl

# add local files
COPY root /

# Set working directory
WORKDIR /app

# Copy the entrypoint script into the container
COPY entrypoint.sh /app/entrypoint.sh

# Make the entrypoint script executable
RUN chmod +x /app/entrypoint.sh

# Ensure correct permissions for all scripts in s6-overlay directory
RUN find /etc/s6-overlay/ -type f -exec chmod 744 {} \; && \
    chmod 744 /docker-mods

VOLUME /config

ENTRYPOINT ["/app/entrypoint.sh"]
