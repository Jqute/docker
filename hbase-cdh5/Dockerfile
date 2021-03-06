FROM centos:centos6
MAINTAINER Olesia Daderko <jqute1@gmail.com>

#=======================
# Install utils
#=======================
COPY install-default.sh install-default.sh
RUN ["/bin/bash", "install-default.sh"]


#=======================
# Install JDK8
#=======================
COPY install-jdk8.sh install-jdk8.sh
RUN ["/bin/bash", "install-jdk8.sh"]

#=======================
# Install CDH 5.4.4 + HBase
#=======================
# ref : http://www.cloudera.com/content/cloudera-content/cloudera-docs/CDH5/latest/CDH5-Quick-Start/cdh5qs_yarn_pseudo.html
COPY install-cdh5-hbase.sh install-cdh5-hbase.sh
RUN ["/bin/bash", "install-cdh5-hbase.sh"]

#=======================
# Configure HBase pseduo-distributed
#=======================

COPY setup.sh setup.sh
COPY hbase-site.xml /etc/hbase/conf/hbase-site.xml
COPY core-site.xml /etc/hadoop/conf/core-site.xml
RUN ["/bin/bash", "setup.sh"]

#=======================
# Start services.
#=======================
COPY start.sh start.sh
# zookeeper
EXPOSE 2181
# HBase master
EXPOSE 60000
# HBase master web UI
EXPOSE 60010
# HBase regionserver
EXPOSE 60020
# HBase regionserver web UI
EXPOSE 60030
CMD ["/bin/bash", "start.sh"]

