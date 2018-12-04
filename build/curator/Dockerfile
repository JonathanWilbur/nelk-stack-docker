FROM centos:latest
LABEL maintainer "Jonathan M. Wilbur <jonathan@wilbur.space>"

# Steps taken directly from here:
# https://www.elastic.co/guide/en/elasticsearch/client/curator/current/yum-repository.html
RUN rpm --import https://packages.elastic.co/GPG-KEY-elasticsearch
ADD ./curator.repo /etc/yum.repos.d/
RUN yum install -y elasticsearch-curator

# Cron is not installed by default on CentOS 7 anymore.
RUN yum install -y cronie

# This fixes this issue: https://github.com/elastic/curator/issues/1243.
RUN echo 'LC_ALL=en_US.UTF-8' >> /etc/crontab
# This cron line means "run at 03:30 every day."
RUN echo '30 3 * * * nobody /usr/bin/curator --config /config.yml /actions.yml' >> /etc/crontab

CMD /usr/sbin/crond -n