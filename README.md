# RBAC

If role-based access control (RBAC) is enabled in your cluster, you may need to give Tiller (the server-side component of Helm) additional permissions. If RBAC is not enabled, be sure to set rbacEnable to false when installing the chart.

```ecma script level 4
# Create a ServiceAccount for Tiller in the `kube-system` namespace
kubectl --namespace kube-system create sa tiller

# Create a ClusterRoleBinding for Tiller
kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller

# Patch Tiller's Deployment to use the new ServiceAccount
kubectl --namespace kube-system patch deploy/tiller-deploy -p '{"spec": {"template": {"spec": {"serviceAccountName": "tiller"}}}}'
```

# install rook operator

```ecma script level 4
 # helm install --namespace rook-ceph --name rook-ceph rook-ceph/
```

# set node selector for three osd nodes


 kubectl label nodes node1 `ceph-osd=enabled`
 
 kubectl label nodes node2 `ceph-osd=enabled` 
  
 kubectl label nodes node3 `ceph-osd=enabled`


# install ceph cluster

```ecma script level 4
 # helm install --namespace rook-ceph --name ceph-cluster ceph-cluster/
```

# check

```ecma script level 4
# kubectl get pods -nrook-ceph
NAME                                      READY   STATUS      RESTARTS   AGE
rook-ceph-agent-4pnmn                     1/1     Running     0          155m
rook-ceph-agent-9wmtf                     1/1     Running     0          155m
rook-ceph-mgr-a-6fbdf695f-p7n6d           1/1     Running     0          8m18s
rook-ceph-mon-a-79475db7f-xh4ql           1/1     Running     0          8m27s
rook-ceph-operator-bdfccf749-p7jms        1/1     Running     0          155m
rook-ceph-osd-0-6b5ff4c85f-clmfp          1/1     Running     0          7m55s
rook-ceph-osd-1-94d67664c-cb8ns           1/1     Running     0          7m54s
rook-ceph-osd-prepare-master-node-d7rtr   0/2     Completed   0          8m15s
rook-ceph-osd-prepare-node1-frqlt         0/2     Completed   0          8m15s
rook-ceph-tools-7c4f75b579-xh8lf          1/1     Running     0          8m42s
rook-discover-dxcb6                       1/1     Running     0          155m
rook-discover-t5v8t                       1/1     Running     0          155m

```