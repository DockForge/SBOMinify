FROM dublok/base-linux:alpine-v1

# Metadata as labels
LABEL org.opencontainers.image.source=""
LABEL org.opencontainers.image.source=https://github.com/DockForge/SBOMinify
LABEL org.opencontainers.image.description="A Docker image to capture and list installed packages and their versions in a Docker image."
LABEL org.opencontainers.image.licenses=GPL-3.0
LABEL maintainer="Dublok"
LABEL description="A Docker image to capture and list installed packages and their versions in a Docker image."

# Set working directory
WORKDIR /app

# Install required packages and syft in a single layer
RUN apk add --no-cache curl bash jq && \
    curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sh -s -- -b /usr/local/bin && \
    apk del curl

# Copy the entrypoint script into the container
COPY entrypoint.sh /app/entrypoint.sh

# Make the entrypoint script executable
RUN chmod +x /app/entrypoint.sh

# Set the entrypoint
ENTRYPOINT ["/app/entrypoint.sh"]