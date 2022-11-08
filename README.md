# run-pod-on-specefic-node

Here are the possible List
1. node selector with node labels
2. node affinity
3. the nodeName field
4. Pod topology spread constraints

1. Node Selector Pod definition:
spec:
 containers:
 - name: nginx
 image: nginx
 nodeSelector:
 disktype: ssd
---
2. Node Name Pod definition:
spec:
 containers:
 - name: nginx
 image: nginx
 nodeName: kube-01
---
3. Node affinity Pod definition:
spec:
 affinity:
 nodeAffinity:
 requiredDuringSchedulingIgnoredDuringExecution:
 nodeSelectorTerms:
 - matchExpressions:
 - key: topology.kubernetes.io/zone
 operator: In
 values:
 - antarctica-east1
 preferredDuringSchedulingIgnoredDuringExecution:
 - weight: 1
 preference:
 matchExpressions:
 - key: another-node-label-key
 operator: In
 values:
 - another-node-label-value
---
4. Pod Topology Spread Constraint 
spec:
 topologySpreadConstraints:
 - maxSkew: <integer>
 minDomains: <integer>
 topologyKey: <string>
 whenUnsatisfiable: <string>
 labelSelector: <object>
 matchLabelKeys: <list>
 nodeAffinityPolicy: [Honor|Ignore]
 nodeTaintsPolicy: [Honor|Ignore]
