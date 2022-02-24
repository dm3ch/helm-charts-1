## MongoDB Standalone

MongDB is a NoSQL based distributed database, this helm chart is for only standalone setup. This helm chart needs [MongoDB Operator](../mongodb-operator) inside Kubernetes cluster. The mongodb definition can be modified or changed by [values.yaml](./values.yaml).

```shell
$ helm repo add ot-helm https://ot-container-kit.github.io/helm-charts/
$ helm install <my-release> ot-helm/mongodb --namespace <namespace>
```

Redis setup can be upgraded by using `helm upgrade` command:-

```shell
$ helm upgrade <my-release> ot-helm/mongodb --install --namespace <namespace>
```

For uninstalling the chart:-

```shell
$ helm delete <my-release> --namespace <namespace>
```

### Pre-Requisities

- Kubernetes => 1.15
- Helm => 3.X
- MongoDB Operator => 0.1.0

### Parameters

| **Name**                                  |        **Value**         | **Description**                                    |
|-------------------------------------------|:------------------------:|----------------------------------------------------|
| `image.name`                              |  quay.io/opstree/mongo   | Name of the MongoDB image                          |
| `image.tag`                               |           v5.0           | Tag for the MongoDB image                          |
| `image.imagePullPolicy`                   |       IfNotPresent       | Image Pull Policy of the MongoDB                   |
 | `image.pullSecret`                        |            ""            | Image Pull Secret for private registry             |
| `resources`                               |            {}            | Request and limits for MongoDB statefulset         |
| `storage.enabled`                         |           true           | Storage is enabled for MongoDB or not              |
| `storage.accessModes`                     |    ["ReadWriteOnce"]     | AccessMode for storage provider                    |
| `storage.storageSize`                     |           1Gi            | Size of storage for MongoDB                        |
| `storage.storageClass`                    |           gp2            | Name of the storageClass to create storage         |
| `mongoDBMonitoring.enabled`               |           true           | MongoDB exporter should be deployed or not         |
| `mongoDBMonitoring.image.name`            | bitnami/mongodb-exporter | Name of the MongoDB exporter image                 |
| `mongoDBMonitoring.image.tag`             |  0.11.2-debian-10-r382   | Tag of the MongoDB exporter image                  |
| `mongoDBMonitoring.image.imagePullPolicy` |       IfNotPresent       | Image Pull Policy of the MongoDB exporter image    |
| `serviceMonitor.enabled`                  |          false           | Servicemonitor to monitor MongoDB with Prometheus  |
| `serviceMonitor.interval`                 |           30s            | Interval at which metrics should be scraped.       |
| `serviceMonitor.scrapeTimeout`            |           10s            | Timeout after which the scrape is ended            |
| `serviceMonitor.namespace`                |        monitoring        | Namespace in which Prometheus operator is running  |
 | `nodeSelector`                            |            {}            | Nodeselector for the MongoDB statefulset           |
 | `priorityClassName`                       |            ""            | Priority class name for the MongoDB statefulset    |
| `affinity`                                |            {}            | Affinity for node and pods for MongoDB statefulset |
| `tolerations`                             |            []            | Tolerations for MongoDB statefulset                |
