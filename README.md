# 3 node Apache Kafka cluster using Docker that demonstrates the Pub-Sub messaging, with a Zookeeper ensemble created to manage the Kafka cluster.

## How to run

1.	Run `sudo docker-compose up -d` at root folder
2.	Add `0.0.0.0 kafka-1 kafka-2 kafka-3` to the client /etc/hosts file
3.	Run `kafkacat -L -b kafka-1:19092` to list all available brokers in the cluster
4.	Create topic by running `docker run --net=host --rm confluentinc/cp-kafka:latest kafka-topics --create --topic cs3219-d --partitions 1 --replication-factor 3 --if-not-exists --zookeeper localhost:32181`
5.	Open two instances of terminal and run `kafkacat -P -b kafka-1:19092 -t cs3219-d` for Producer and `kafkacat -C -b kafka-3:39092 -t cs3219-d` for Consumer
6.	Write some message to the Producer terminal and you should be able to see the same message in the Consumer terminal.

