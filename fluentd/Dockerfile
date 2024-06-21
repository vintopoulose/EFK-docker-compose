FROM ruby:3.0

# Install Fluentd
RUN gem install fluentd -v 1.14.6 --no-document

# Install necessary Ruby gems for Elasticsearch
RUN gem install faraday -v 2.8.1 --no-document
RUN gem install faraday-net_http -v 3.0.2 --no-document

# Install Elasticsearch Ruby gems
RUN gem install elasticsearch -v 7.10.0 --no-document
RUN gem install elasticsearch-transport -v 7.10.0 --no-document
RUN gem install elasticsearch-api -v 7.10.0 --no-document

# Install fluent-plugin-elasticsearch with compatible version
RUN gem install fluent-plugin-elasticsearch -v 4.3.3 --no-document

# Create Fluentd user and directories
RUN useradd -u 1000 -m fluent && \
    mkdir -p /fluentd/log && \
    mkdir -p /fluentd/etc /fluentd/plugins && \
    chown -R fluent /fluentd

USER fluent
WORKDIR /fluentd

# Copy Fluentd configuration file
COPY ./conf/fluent.conf /fluentd/etc/fluent.conf

# Command to run Fluentd
CMD ["fluentd", "-c", "/fluentd/etc/fluent.conf", "-p", "/fluentd/plugins"]
