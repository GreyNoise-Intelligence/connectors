FROM python:3.12-alpine
ENV CONNECTOR_TYPE=INTERNAL_ENRICHMENT

# Copy the connector
COPY src /opt/opencti-connector-rf-enrichment

# Install Python modules
# hadolint ignore=DL3003
RUN apk update && apk upgrade && \
    apk --no-cache add git build-base libmagic libxslt libxslt-dev libxml2 libxml2-dev && \
    cd /opt/opencti-connector-rf-enrichment && \
    pip install --no-cache-dir -r requirements.txt && \
    apk del git build-base libxslt-dev libxml2-dev && \
    rm -rf /var/cache/apk/*

# Expose and entrypoint
COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
