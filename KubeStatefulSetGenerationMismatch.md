

## KubeStatefulSetGenerationMismatch

**Description**
This alert indicates that a Kubernetes statefulset in the cluster is not able to start the desired pods.

**Diagnosis**
Check the status of the stateful set using the kubernetes client (kubectl)

    $ kubectl -n <namespace> describe <statefulsetname>

**Mitigation**
Resolving this issue depends on the cause.

**Example**

    $ kubectl -n pt-my-company-streams-987 describe sts/pf-my-company-streams-987-astracdc-zstra-account-sink
    
      Type     Reason        Age                 From                    Message
    
      ----     ------        ----                ----                    -------

  Warning  FailedCreate  15m (x792 over 8d)  statefulset-controller  create Pod pf-my-company-streams-987-astracdc-zstra-account-sink-0 in StatefulSet pf-my-company-streams-987-astracdc-zstra-account-sink failed error: Pod "pf-my-company-streams-987-astracdc-zstra-account-sink-0" is invalid: metadata.labels: Invalid value: "pf-my-company-streams-987-astracdc-zstra-account-sink-5d4d759bfb": must be no more than 63 characters

In this case, the user created an invalid stateful set because the name was too long.  To resolve this we need to send the user a notification, delete the pulsar sink which generated the statefulset, and add validation checks to astra streaming to prevent this from happening in the future.
