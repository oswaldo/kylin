#
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

# Docker image for apache kylin, based on the Hadoop image
FROM hadoop2.7-all-in-one_sqoop:latest

ENV KYLIN_VERSION 3.1.0
ENV KYLIN_HOME /home/admin/apache-kylin-$KYLIN_VERSION-bin-hbase1x

# Download released Kylin
RUN wget https://archive.apache.org/dist/kylin/apache-kylin-$KYLIN_VERSION/apache-kylin-$KYLIN_VERSION-bin-hbase1x.tar.gz \
    && tar -zxvf /home/admin/apache-kylin-$KYLIN_VERSION-bin-hbase1x.tar.gz \
    && rm -f /home/admin/apache-kylin-$KYLIN_VERSION-bin-hbase1x.tar.gz

RUN cp $HIVE_HOME/hcatalog/share/hcatalog/hive-hcatalog-core-1.2.1.jar $SPARK_HOME/jars/

COPY conf/kylin/kylin.properties ${KYLIN_HOME}/conf

RUN cp $SQOOP_LIB_DIR/mysql-connector-java-$MYSQL_CONNECCTOR_VERSION.jar ${KYLIN_HOME}/ext

COPY ./entrypoint.sh /home/admin/entrypoint.sh
RUN chmod u+x /home/admin/entrypoint.sh

ENTRYPOINT ["/home/admin/entrypoint.sh"]
