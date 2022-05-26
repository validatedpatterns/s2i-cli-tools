FROM registry.access.redhat.com/ubi8/ubi

MAINTAINER `team-validated-patterns@redhat.com`

USER root

RUN dnf install --disableplugin=subscription-manager --nodocs jq -y && \
    dnf clean all && \
    rm -rf /var/run/cache

USER 1001
