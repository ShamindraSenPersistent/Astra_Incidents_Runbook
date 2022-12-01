
## KubePersistentVolumeFillingUp

**Description**  
The alert indicates that a pulsar broker pod in the Kubernetes cluster is filling up.

**Diagnosis**  
Check the status of the disk space in the shell of pvc.  
df -h

**Mitigation**  
It was found out that Journal/ledgers were filling up which makes more evident to increase the Volume  
Steps taken:
-   Changed pvc storage for pulsar-gcp-australiase1-bookkeeper-journal-pulsar-gcp-australiase1-bookkeeper-2 from 50Gi to 100Gi.
    

**Example**

    Labels:  
    - alertname = KubePersistentVolumeFillingUp  
    - endpoint = https-metrics  
    - instance = 10.152.0.49:10250  
    - job = kubelet  
    - metrics_path = /metrics  
    - namespace = pulsar  
    - node = gke-astra-streaming-prod-default-pool-50ed3ca6-u5ia  
    - persistentvolumeclaim = pulsar-gcp-australiase1-bookkeeper-journal-pulsar-gcp-australiase1-bookkeeper-2  
    - prometheus = pulsar/astraproduction-gcp-pulsar-prometheus  
    - service = astraproduction-gcp-pulsar-kubelet  
    - severity = critical  
    Annotations:  
    - message = The PersistentVolume claimed by pulsar-gcp-australiase1-bookkeeper-journal-pulsar-gcp-australiase1-bookkeeper-2 in Namespace pulsar is only 9.972% free

.

Source: [https://prometheus.gcp-australiase1.streaming.datastax.com/graph?g0.expr=kubelet_volume_stats_available_bytes%7Bjob%3D%22kubelet%22%2Cmetrics_path%3D%22%2Fmetrics%22%2Cnamespace%3D~%22.%2A%22%7D+%2F+kubelet_volume_stats_capacity_bytes%7Bjob%3D%22kubelet%22%2Cmetrics_path%3D%22%2Fmetrics%22%2Cnamespace%3D~%22.%2A%22%7D+%3C+0.1&g0.tab=1](https://prometheus.gcp-australiase1.streaming.datastax.com/graph?g0.expr=kubelet_volume_stats_available_bytes%7Bjob%3D%22kubelet%22%2Cmetrics_path%3D%22%2Fmetrics%22%2Cnamespace%3D~%22.%2A%22%7D+%2F+kubelet_volume_stats_capacity_bytes%7Bjob%3D%22kubelet%22%2Cmetrics_path%3D%22%2Fmetrics%22%2Cnamespace%3D~%22.%2A%22%7D+%3C+0.1&g0.tab=1)