## alluxio and minio deployment

AlluxIO requires /tmp/domain to be available through the kubelet.

First create the config map
```
kubectl create configmap alluxio-config --from-file=ALLUXIO_CONFIG=conf/alluxio.properties
```

Next create the minio deployment
```
kubectl apply -f minio-deployment.yaml
```

Follow-up with deployment of storage PV and deployment of AlluxIO master
```
kubectl apply -f alluxio-journal-volume.yaml
kubectl apply -f alluxio-master.yaml
```

Finish the the deployment of the AlluxIO workers. This is a deamon set which will deploy on ALL nodes.
```
kubectl apply -f alluxio-worker.yaml
```


