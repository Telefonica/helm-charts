# HDFS Chart

[HDFS](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsUserGuide.html) is the primary distributed storage used by Hadoop applications.

## Chart Details

## Installing the Chart

To install the chart with the release name `hdfs-test`:

```
$ helm install --name hdfs-test hdfs
```

### Persistence

To install the chart with persistent volumes:

```
$ helm install --name hdfs-test \
  --set persistence.nameNode.enabled=true \
  --set persistence.nameNode.storageClass=standard \
  --set persistence.dataNode.enabled=true \
  --set persistence.dataNode.storageClass=standard \
  hdfs
```

> Change the value of `storageClass` to match your volume driver. `standard` works for Google Container Engine clusters.

## Configuration

The following table lists the configurable parameters of the HDFS chart and their default values.

| Parameter                                         | Description                                                                        | Default                                                          |
| ------------------------------------------------- | -------------------------------                                                    | ---------------------------------------------------------------- |
| `image`                                           | Hadoop image ([source](https://github.com/Comcast/kube-yarn/tree/master/image))    | `danisla/hadoop:{VERSION}`                                       |
| `imagePullPolicy`                                 | Pull policy for the images                                                         | `IfNotPresent`                                                   |
| `hadoopVersion`                                   | Version of hadoop libraries being used                                             | `{VERSION}`                                                      |
| `antiAffinity`                                    | Pod antiaffinity, `hard` or `soft`                                                 | `hard`                                                           |
| `hdfs.nameNode.pdbMinAvailable`                   | PDB for HDFS NameNode                                                              | `1`                                                              |
| `hdfs.nameNode.resources`                         | resources for the HDFS NameNode                                                    | `requests:memory=256Mi,cpu=10m,limits:memory=2048Mi,cpu=1000m`   |
| `hdfs.dataNode.replicas`                          | Number of HDFS DataNode replicas                                                   | `1`                                                              |
| `hdfs.dataNode.pdbMinAvailable`                   | PDB for HDFS DataNode                                                              | `1`                                                              |
| `hdfs.dataNode.resources`                         | resources for the HDFS DataNode                                                    | `requests:memory=256Mi,cpu=10m,limits:memory=2048Mi,cpu=1000m`   |
| `persistence.nameNode.enabled`                    | Enable/disable persistent volume                                                   | `false`                                                          |
| `persistence.nameNode.storageClass`               | Name of the StorageClass to use per your volume provider                           | `-`                                                              |
| `persistence.nameNode.accessMode`                 | Access mode for the volume                                                         | `ReadWriteOnce`                                                  |
| `persistence.nameNode.size`                       | Size of the volume                                                                 | `50Gi`                                                           |
| `persistence.dataNode.enabled`                    | Enable/disable persistent volume                                                   | `false`                                                          | 
| `persistence.dataNode.storageClass`               | Name of the StorageClass to use per your volume provider                           | `-`                                                              |
| `persistence.dataNode.accessMode`                 | Access mode for the volume                                                         | `ReadWriteOnce`                                                  |
| `persistence.dataNode.size`                       | Size of the volume                                                                 | `200Gi`                                                          |


# References

- Original K8S Hadoop adaptation this chart was derived from: https://github.com/helm/charts/tree/master/stable/hadoop
