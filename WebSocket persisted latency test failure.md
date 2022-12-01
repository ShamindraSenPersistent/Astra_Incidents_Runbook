

## WebSocket persisted latency test failure

**Description**  
The alert indicates that WebSocket persisted latency test failure.

**Diagnosis**  
Checked whether core  DNS pod and svc is running or not.
Further checking the logs of core DNS pod

**Mitigation**
It was found that Journal/ledgers were filling up.  
Steps taken: 
-   DNS Restart/proxy restart      

**Example**