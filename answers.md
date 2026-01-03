```
broker:/opt/kafka/bin$ ./kafka-topics.sh --create --topic practise-topic --bootstrap-server broker:9092 --partitions 3 --replication-factor 1
Created topic practise-topic.

broker:/opt/kafka/bin$ 
broker:/opt/kafka/bin$ ./kafka-topics.sh  --topic practise-topic --bootstrap-server broker:9092 --list
practise-topic

broker:/opt/kafka/bin$ 
broker:/opt/kafka/bin$ ./kafka-topics.sh --create --topic dead-letter-topic --bootstrap-server broker:9092 --partitions 1 --replication-factor 1
Created topic dead-letter-topic.

broker:/opt/kafka/bin$ 
broker:/opt/kafka/bin$ ./kafka-topics.sh  --topic dead-letter-topic --bootstrap-server broker:9092 --describe
Topic: dead-letter-topic	TopicId: Ptbv6kzIQv6xk2JXCewdeA	PartitionCount: 1	ReplicationFactor: 1	Configs: 
	Topic: dead-letter-topic	Partition: 0	Leader: 1	Replicas: 1	Isr: 1	Elr: 	LastKnownElr: 

broker:/opt/kafka/bin$ ./kafka-topics.sh  --topic practise-topic  --bootstrap-server broker:9092 --describe
Topic: practise-topic	TopicId: 4sYb_q80RZGfkh6cLLJZqg	PartitionCount: 3	ReplicationFactor: 1	Configs: 
	Topic: practise-topic	Partition: 0	Leader: 1	Replicas: 1	Isr: 1	Elr: 	LastKnownElr: 
	Topic: practise-topic	Partition: 1	Leader: 1	Replicas: 1	Isr: 1	Elr: 	LastKnownElr: 
	Topic: practise-topic	Partition: 2	Leader: 1	Replicas: 1	Isr: 1	Elr: 	LastKnownElr: 



broker:/opt/kafka/bin$ ./kafka-console-producer.sh --topic practise-topic --bootstrap-server broker:9092 --property "parse.key=true" --property "key.separator=:"
>key1 : Message for Partition1
>key2 : Message for Partition2
>key3 : Message for Partition3
>key4: Message for Partition4
>key5: Message for Partition5                                
>key6: Message for Partition6
>key7: Message for Partition8

broker:/opt/kafka/bin$ ./kafka-console-producer.sh --topic practise-topic --bootstrap-server broker:9092 --property "parse.key=true" --property "key.separator=:"
>key1 : Message for Partition1
>key2 : Message for Partition2
>key3 : Message for Partition3
>key1 : Message for Partition1
>key2 : Message for Partition2
>key3 : Message for Partition3

```
```
Consumer

broker:/opt/kafka/bin$ ./kafka-console-consumer.sh --topic practise-topic --bootstrap-server broker:9092 --group group-A
 Message for Partition1
 Message for Partition2
 Message for Partition3

```

```
broker:/opt/kafka/bin$ ./kafka-topics.sh  --topic practise-topic  --bootstrap-server broker:9092 --describe
Topic: practise-topic	TopicId: 4sYb_q80RZGfkh6cLLJZqg	PartitionCount: 3	ReplicationFactor: 1	Configs: 
	Topic: practise-topic	Partition: 0	Leader: 1	Replicas: 1	Isr: 1	Elr: 	LastKnownElr: 
	Topic: practise-topic	Partition: 1	Leader: 1	Replicas: 1	Isr: 1	Elr: 	LastKnownElr: 
	Topic: practise-topic	Partition: 2	Leader: 1	Replicas: 1	Isr: 1	Elr: 	LastKnownElr: 
broker:/opt/kafka/bin$ 
broker:/opt/kafka/bin$ ./kafka-topics.sh  --topic practise-topic  --bootstrap-server broker:9092 --describe
Topic: practise-topic	TopicId: 4sYb_q80RZGfkh6cLLJZqg	PartitionCount: 3	ReplicationFactor: 1	Configs: 
	Topic: practise-topic	Partition: 0	Leader: 1	Replicas: 1	Isr: 1	Elr: 	LastKnownElr: 
	Topic: practise-topic	Partition: 1	Leader: 1	Replicas: 1	Isr: 1	Elr: 	LastKnownElr: 
	Topic: practise-topic	Partition: 2	Leader: 1	Replicas: 1	Isr: 1	Elr: 	LastKnownElr: 
broker:/opt/kafka/bin$ ./kafka-console-consumer.sh --topic practise-topic --bootstrap-server broker:9092 --property print.partition=true --property print.key=true 
Partition:0	key4	 Message for Partition4
Partition:1	key5	 Message for Partition5
Partition:0	key6	 Message for Partition6
Partition:0	key7	 Message for Partition8


```

```
ubuntu@ip-172-31-34-13:~$ docker exec -it -w /opt/kafka/bin broker bash
broker:/opt/kafka/bin$ 
broker:/opt/kafka/bin$ ./kafka-console-consumer.sh --topic practise-topic --bootstrap-server broker:9092 --group group-A
 Message for Partition4
 Message for Partition5 
 Message for Partition2

```

```
ubuntu@ip-172-31-34-13:~$ docker exec -it -w /opt/kafka/bin broker bash
broker:/opt/kafka/bin$ ./kafka-console-consumer.sh --topic practise-topic --bootstrap-server broker:9092 --group group-B
 Message for Partition1
 Message for Partition2
 message for Partition3
 Message for partition2

```

```
broker:/opt/kafka/bin$ ./kafka-console-consumer.sh --topic practise-topic --bootstrap-server broker:9092  --partition 1 --from-beginning
 Message for Partition1
 Message for Partition5
 Message for Partition1
 Message for Partition1
 Message for Partition1
 Message for Partition6
 Message for Partition6
 Message for Partition1
^CProcessed a total of 8 messages
broker:/opt/kafka/bin$ 
broker:/opt/kafka/bin$ ./kafka-console-consumer.sh --topic practise-topic --bootstrap-server broker:9092  --partition 0 --from-beginning
 Message for Partition4
 Message for Partition6
 Message for Partition8
 Message for Partition1
 Message for partition2
 Message for partition2
^CProcessed a total of 6 messages
broker:/opt/kafka/bin$ 
broker:/opt/kafka/bin$ 
broker:/opt/kafka/bin$ ./kafka-console-consumer.sh --topic practise-topic --bootstrap-server broker:9092 | while read msg
> do
>  if [["$msg" == *"error"*]];then
>    echo "$msg" | ./kafka-console-producer.sh --topic dead-letter-topic --bootstrap-server broker:9092 
>  fi
> done

```


```
broker:/opt/kafka/bin$ ./kafka-consumer-groups.sh  --bootstrap-server broker:9092 --describe --group group-A --group -B
```
