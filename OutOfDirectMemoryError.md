
## Pulsar component OutOfDirectMemoryError

**Description**

The alert indicates that a particular pulsar component is running short of memory due to heavy traffic in the node.

**Diagnosis**

Look into New-relic logs to identify the faulty component.

For further clarification check the logs of broker, bookkeeper, and zookeeper in Grafana by port forwarding the Grafana pod present in the same cluster for which the alert is raised.

**Mitigation**

After thorough investigation it was found to be an issue in the pulsar broker pods present in the cluster.

This alert arose due to heavy message transfer that directly affects Direct Memory.

So, rolling restart  the broker node from k9s to mitigate the issue.

**Example**

    Alert Condition Names, Pulsar component OutOfDirectMemoryError alert
    
    Alert Policy Names, Pulsar component OOM
    
    Description, Policy: 'Pulsar component OOM'. Condition: 'Pulsar component OutOfDirectMemoryError alert'
    
    Impacted Entities, Log query

IssueURL, https://radar-api.service.newrelic.com/accounts/3201025/issues/2416b0d0-c4ce-49cf-8ee5-4e21ab76ebc9?notifier=PAGERDUTY_ACCOUNT_INTEGRATION
