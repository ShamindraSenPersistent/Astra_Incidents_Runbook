## missing-function-critical

**Description**

The alert indicates that a pulsar function pod in the  Kubernetes cluster is terminating.

**Diagnosis**

Look for the pulsar function pod causing the error from the statefulset using any Kubernetes client (kubectl or k9s)

```$ kubectl –n <namespace> describe <statefulsetname>```

**Mitigation**

After diagnosis it was found that pulsar-aws-useast1-function-0 belonging to the node mentioned in the pager message was terminating repeatedly.

Function worker was missing alert rule. So, add namespace constraint it.

**Example**

```Labels:  
- alertname = missing-function-critical  
- prometheus = pulsar/astraproduction-aws-useast-prometheus  
- severity = critical  
Annotations:  
- description = missing function replicas```  
Source: [https://prometheus.aws-useast1.streaming.datastax.com/graph?g0.expr=count%28up%7Bjob%3D%22function%22%7D+%3D%3D+1%29+%2F+count%28up%7Bjob%3D%22function%22%7D%29+%21%3D+1&g0.tab=1](https://prometheus.aws-useast1.streaming.datastax.com/graph?g0.expr=count%28up%7Bjob%3D%22function%22%7D+%3D%3D+1%29+%2F+count%28up%7Bjob%3D%22function%22%7D%29+%21%3D+1&g0.tab=1)
