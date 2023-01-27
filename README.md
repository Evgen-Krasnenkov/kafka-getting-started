# DOCKER
1. Please make sure that Docker is already installed in the system,
   If not, install from https://www.docker.com/products/docker-desktop

2. If on Windows O/S, open a Powershell window.
   If on Mac OS or Linux, open a Terminal window.

3. Navigate to the directory where the exercise files are downloaded.
   This directory would contain the kafka-single-node.yml file

4. Execute the following command from this directory

        docker-compose -f kafka-single-node.yml up -d

5. Check if the containers are up and running

        docker ps


6. To shutdown and remove the setup, execute this command in the same directory

        docker-compose -f kafka-single-node.yml down

# KAFKA DOCS
    https://kafka.apache.org/documentation/#brokerconfigs

### This section contains the shell commands for the Kafka Essentials:

## Logging into the Kafka Container

        docker exec -it kafka-broker /bin/bash

## Logging into the Kafka ZooKeeper

        docker exec -it zookeeper /bin/bash
        cd /opt/bitnami/zookeeper/bin/
        ./zkCli.sh
        ls /brokers/ids
        get /brokers/ids/1001
        ls /brokers/topics
        get /brokers/topics/kafka.learning.tweets

        ps -ef |grep kafka
        cat /opt/bitnami/kafka/config/server.properties

## Navigate to the Kafka Scripts directory

        cd /opt/bitnami/kafka/bin

## Creating new Topics - DEPRECIATED

        ./kafka-topics.sh \
            --zookeeper zookeeper:2181 \
            --create \
            --topic kafka.learning.tweets \
            --partitions 1 \
            --replication-factor 1

        ./kafka-topics.sh \
                        --zookeeper zookeeper:2181 \
                        --create \
                        --topic kafka.learning.alerts \
                        --partitions 1 \
                        --replication-factor 1

## Creating new Topics with bootstrap

        ./kafka-topics.sh \
            --create \
            --topic kafka.learning.tweets \
            --bootstrap-server localhost:9092 \
            --partitions 1 \
            --replication-factor 1

        ./kafka-topics.sh \
            --create \
            --topic kafka.learning.alerts \
            --bootstrap-server localhost:9092 \
            --partitions 1 \
            --replication-factor 1

## Listing Topics - DEPRECIATED

        ./kafka-topics.sh \
            --zookeeper zookeeper:2181 \
            --list \

## Listing Topics

        ./kafka-topics.sh \
            --list \
            --bootstrap-server localhost:9092

## Getting details about a Topic DEPRECIATED

        ./kafka-topics.sh \
            --zookeeper zookeeper:2181 \
            --describe
## Getting details about a Topic with Bootstrap

        ./kafka-topics.sh \
            --describe \
            --bootstrap-server localhost:9092

## Publishing Messages to Topics

        ./kafka-console-producer.sh \
            --bootstrap-server localhost:29092 \
            --topic kafka.learning.tweets

## Consuming Messages from Topic

        ./kafka-console-consumer.sh \
            --bootstrap-server localhost:29092 \
            --topic kafka.learning.tweets \
            --from-beginning

## Deleting Topics DEPRECIATED

        ./kafka-topics.sh \
            --zookeeper zookeeper:2181 \
            --delete \
            --topic kafka.learning.alerts

## Deleting Topics with Bootstrap

        ./kafka-topics.sh \
            --bootstrap-server localhost:29092 \
            --delete \
            --topic kafka.learning.alerts