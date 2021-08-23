# AKS-Kube-system-log-to-loganalytics
This article intended to push kube-system logs to log analytics workspace in AKS

To enable kube-system logs to be pushed to Log analytics you can do below steps:
 
1.	Download the above configmap.
2.	Apply the configmap with the below:

kubectl apply -f configmap-oms.yaml
3.	Recreate omsagent pods to take effect:

kubectl delete pods -n kube-system -l component=oms-agent

Wait for a few minutes and you can verify that you started to get logs. You can verify that you started to get the logs with the below query which will show you the time where the first event has been logged for tunnelfront as an example.

ContainerLog
| where  Image contains "tunnel"
| summarize arg_min(TimeGenerated, *)

