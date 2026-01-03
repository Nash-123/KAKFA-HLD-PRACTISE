## Task 1: Create Topics
1. Create two Kafka topics:
   - practice-topic with 3 partitions
   - dead-letter-topic with 1 partition
2. Verify the topics using Kafka CLI

---

## Task 2: Produce Messages
1. Produce messages to practice-topic with key-value pairs:
   - key1: Message for Partition 1
   - key2: Message for Partition 2
   - key3: Message for Partition 3
2. Observe which partition each message is sent to

---

## Task 3: Consume Messages Using Consumer Group
1. Create consumer group group-A with 3 consumers
2. Verify each consumer is assigned one partition
3. Add another consumer to group-A and observe rebalance
4. Create consumer group group-B with 2 consumers and observe partition distribution

---

## Task 4: Manual Partition Assignment
1. Assign a single consumer to read from partitions 0 and 1
2. Produce messages and confirm only those partitions are consumed

---

## Task 5: Simulate and Handle Processing Failures
1. Simulate failure for messages containing the word "error"
2. Send failed messages to dead-letter-topic

---

## Task 6: Dead Letter Queue Consumer
1. Consume messages from dead-letter-topic
2. Print message with metadata (timestamp, partition)

---

## Task 7: Monitoring and Troubleshooting
1. Describe consumer groups group-A and group-B
2. Document partition lag

---

## Bonus Task: Custom Partitioning
1. Implement custom partition logic:
   - Keys starting with "A" → Partition 0
   - Keys starting with "B" → Partition 1
   - Others → Partition 2
2. Verify partition assignment
