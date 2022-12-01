## CDC StuckPartitionOrTopic

**Description**
This indicates that pulsar clients are connected to a topic, but are not consuming messages.  This could indicate a client issue, or could be a problem in pulsar.

**Diagnosis**
Check the pulsar unacked message per subscription of the CDC topic. If it is over 190,000, the consumers are not acking the message.
Broker log should also have some lines like `Dispatcher read is blocked due to unackMessages 200010 reached to max 200000
There is no redelivery on the subscription.

**Mitigation**
Collect the topic stats, stats-internal and broker logs
Take heapdump and stacktrace of broker that owns the topic. The CDC topis is a partitioned topic. It has at least three partitions. So we need to find all the brokers owns them.
Page DBPE to take a heap dump and stack trace of CDC service. Ask them to perform [https://github.com/riptano/cndb/blob/master/kubernetes/ops/runbooks/debug_cndb_service.md](https://github.com/riptano/cndb/blob/master/kubernetes/ops/runbooks/debug_cndb_service.md) 
There might be 3 cdc service pods so we need collect Pulsar client's heapdump and stacktrace from all of these pods.
The CDC topis is a partitioned topic. It has at least three partitions. So we need to find all the brokers owns them.
 then unload the topic.