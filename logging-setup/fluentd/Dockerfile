# Dockerfile for add fluentd plugins. Must be in docker-compose fluentd service context
# Ref: https://github.com/marcel-dempers/docker-development-youtube-series/blob/master/monitoring/logging/fluentd/introduction/dockerfile#L1
FROM fluent/fluentd:v1.11-debian

USER root
# ref for more output plugins: https://docs.fluentd.org/output/opensearch
RUN gem install fluent-plugin-opensearch
