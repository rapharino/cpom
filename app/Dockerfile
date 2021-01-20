# Set the base image to Centos 7
FROM centos:7

# Update the repository sources list
RUN yum -y --setopt=tsflags=nodocs update

# -----------------------------------------------------------------------------
# Install dnsmasq
# -----------------------------------------------------------------------------
RUN yum -y install dnsmasq

# -----------------------------------------------------------------------------
# Install MySQL Client
# -----------------------------------------------------------------------------
RUN yum -y --setopt=tsflags=nodocs install Percona-Server-client-57

# -----------------------------------------------------------------------------
# Install Orchestrator
# -----------------------------------------------------------------------------

COPY orchestrator.conf.json /etc/orchestrator.conf.json
RUN chown root:root /etc/orchestrator.conf.json && \
    chmod a+x /etc/orchestrator.conf.json

COPY entrypoint.sh /root/entrypoint.sh
RUN chmod a+x /root/entrypoint.sh

# -----------------------------------------------------------------------------
# Clear
# -----------------------------------------------------------------------------
RUN yum -y clean all && \
    rm -rf /var/cache/yum/*
############################## INSTALLATION END ###############################

# Set the working directory to /var/www
WORKDIR /root

# Expose the default http port
EXPOSE 3000/tcp

# Start service on run container
ENTRYPOINT ["/root/entrypoint.sh"]
