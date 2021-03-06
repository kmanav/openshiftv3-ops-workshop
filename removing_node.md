# Removing a node
In this lab you will safely remove a node from the Openshift Cluster.


$ oc get nodes

## determine the node you want to remove, make it unschedulable
$ oc adm manage-node <node>  --schedulable=false
## ensure it is correctly labeled as unschedulable
$ oc get nodes
## e.g.
## ip-172-31-21-67.us-east-2.compute.internal    Ready,SchedulingDisabled   compute   10d       v1.9.1+a0ce1bc657
## evacuate pods
$ oc adm drain <node> --ignore-daemonsets --delete-local-data --force
## check that the node has no running pods
$ oc adm manage-node <node> --list-pods
## delete nodes
$ oc delete node <node>
