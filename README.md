Assumptions.
# Docker is installed in local/Linux. This is more geared to mac. Windows might be little different. 
# python > 3.8 and pip are installed locally.
# Do not run from OneDrive - Southwest Airlines or do volume mapping on docker.
# If we are restarting docker zookeper/kafka container, delete the data directory. 
# if you have errors as "no space left" clean up all containers and images from docker. 

1. Clone the existing repository.

2. export DOCKER_DEFAULT_PLATFORM=linux/amd64
3. docker-compose up 
4. docker ps 

CONTAINER ID   IMAGE                       COMMAND                  CREATED       STATUS       PORTS                                         NAMES
4a0aa8322b13   confluentinc/cp-kafka       "/etc/confluent/dock…"   2 hours ago   Up 2 hours   9092/tcp, 0.0.0.0:9091->9091/tcp, 19091/tcp   broker1
c7cccf79ac6c   confluentinc/cp-zookeeper   "/etc/confluent/dock…"   2 hours ago   Up 2 hours   2888/tcp, 0.0.0.0:2181->2181/tcp, 3888/tcp    zookeeper

6. To run producer/consumer manually from the docker container, 

In one terminal - docker exec --interactive --tty broker1 kafka-console-producer --bootstrap-server broker1:9091  --topic quickstart

Enter some text and enter, enter more text and enter. 

7. To run the consumer, open another terminal. 
docker exec --interactive --tty broker1 kafka-console-consumer --bootstrap-server broker1:9091  --topic quickstart  --from-beginning

You should be able to see all the messages from the other terminal. 

8. To run the producer/consumer as a python script, run pip3 install -r requirements.txt
9. Run Producer as python3 ./producer.py --topic=quickstart --key=broker1
10. To run as consumer, run as python3 ./consumer.py 