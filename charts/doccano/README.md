# Doccano

Doccano is an open source text annotation tool for humans. It provides annotation features for text classification, sequence labeling and sequence to sequence tasks. So, you can create labeled data for sentiment analysis, named entity recognition, text summarization and so on. Just create a project, upload data and start annotating. You can build a dataset in hours.

To get more informations :

* [Github Source Code](https://github.com/doccano/doccano)
* [Dockerhub Docker Image](https://hub.docker.com/r/doccano/doccano)

## Installing the Chart

Before you can install the chart you will need to add the `curiedfcharts` repo to [Helm](https://helm.sh/).

```shell
helm repo add curiedfcharts https://curie-data-factory.github.io/helm-charts
helm repo update
```

After you've installed the repo you can install the chart.

```shell
helm upgrade --install --namespace default --values ./my-values.yaml my-release curiedfcharts/doccano
```

## Configuration

The following table lists the configurable parameters of the chart and their default values.

| Parameter                        | Description                                                          | Default                                                             |
|----------------------------------|----------------------------------------------------------------------|---------------------------------------------------------------------|
| `image.replicaCount`             | Number of replicas to create                                         | `1`                                                                 |
| `image.repository`               | Image repository.                                                    | `doccano/doccano`                                                   |
| `image.tag`                      | Image Tag.                                                           | `1.2.2`                                                             |
| `image.pullPolicy`               | Image pull policy.                                                   | `IfNotPresent`                                                      |
| `image.name`                     | Image name                                                           | `doccano`                                                           |
| `image.deployRegistry`           | If the image is stored in a private registry                         | `false`                                                             |
| `image.imagePullSecrets`         | Docker registry credentials Secret name                              | `registrysecret`                                                    |
| `image.dataSecret`               | Secret storing docker image registry credentials                     | `{"auths":{"registry.compagny.com":{"password":"","username":""}}}` |
| `env.ADMIN_EMAIL`                | Doccano Admin Email                                                  | `admin@company.com`                                                 |
| `env.ADMIN_USERNAME`             | Doccano Admin Username                                               | `admin`                                                             |
| `deploySecret`                   | Wether or not to deploy the secret containing Doccano ADMIN_PASSWORD | `true`                                                              |
| `ADMIN_PASSWORD`                 | Doccano Admin Password                                               | `password`                                                          |
| `service.type`                   | Service Type                                                         | `ClusterIP`                                                         |
| `service.targetPort`             | Service Port                                                         | `8000`                                                                |
| `service.protocol`               | Service Protocol                                                     | `TCP`                                                               |
| `ingress.enabled`                | Expose application with ingress                                      | `true`                                                              |
| `ingress.hostnames`              | Urls of exposed application                                          | `['doccano.company.com']`                                           |
| `ingress.path`                   | Path through ingress                                                 | `/`                                           |
| `ingress.tls`                    | Array of TLS Hosts                                                   | `[]`                                                                |
| `ingress.tls[hosts]`             | Host name                                                            | `['doccano.company.com']`                                           |
| `ingress.tls[hosts[secretName]]` | Secret for the current host name                                     | `doccano`                                                           |
| `persistence.enabled`            | Enable persisting data on PVC                                        | `false`                                                             |
| `persistence.existingClaim`      | Does PVC already exist ?                                             | `false`                                                             |
| `persistence.size`               | PVC Size                                                             | `10Gi`                                                              |
| `persistence.storageClass`       | PVC storage class                                                    | `nil`                                                               |
| `persistence.accessMode`         | PVC Access Mode                                                      | `ReadWriteOnce`                                                     |
| `persistence.replicas`           | PVC storage class replicas (if possible)                             | `1`                                                                 |
| `persistence.volumeName`         | Directory name                                                       | `data`                                                              |
| `persistence.mountPath`          | Directory mount path                                                 | `/data`                                                             |
