# Nexus

[Nexus OSS](https://www.sonatype.com/nexus-repository-oss) is a free open source repository manager. It supports a wide range of package formats and it's used by hundreds of tech companies.

## Introduction

This chart bootstraps a Nexus OSS deployment on a cluster using Helm.

## Prerequisites

- Kubernetes 1.8+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

### With GCP IAM enabled
All the [Prerequisites](#Prerequisites) should be in place, plus:

## Testing the Chart
To test the chart:
```bash
$ helm install --dry-run --debug ./
```
To test the chart with your own values:
```bash
$ helm install --dry-run --debug -f my_values.yaml ./
```

## Installing the Chart

Before you can install the chart you will need to add the `curiedfcharts` repo to [Helm](https://helm.sh/).

```shell
helm repo add curiedfcharts https://curie-data-factory.github.io/helm-charts
helm repo update
```

After you've installed the repo you can install the chart.

```shell
helm upgrade --install --namespace default --values ./my-values.yaml my-release curiedfcharts/nexus
```

## Uninstalling the Chart

To uninstall/delete the deployment:

```bash
$ helm list
NAME           	REVISION	UPDATED                 	STATUS  	CHART      	NAMESPACE
plinking-gopher	1       	Fri Sep  1 13:19:50 2017	DEPLOYED	sonatype-nexus-0.1.0	default
$ helm delete plinking-gopher
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the chart and their default values.

| Parameter                        | Description                                      | Default                                                             |
|----------------------------------|--------------------------------------------------|---------------------------------------------------------------------|
| `image.replicaCount`             | Number of replicas to create                     | `1`                                                                 |
| `image.repository`               | Image repository.                                | `sonatype/nexus3`                            |
| `image.tag`                      | Image Tag.                                       | `3.30.0`                                                             |
| `image.pullPolicy`               | Image pull policy.                               | `IfNotPresent`                                                      |
| `image.name`                     | Image name                                       | `nexus`                                                  |
| `image.deployRegistry`           | If the image is stored in a private registry     | `false`                                                             |
| `image.imagePullSecrets`         | Docker registry credentials Secret name          | `registrysecret`                                                    |
| `image.dataSecret`               | Secret storing docker image registry credentials | `{"auths":{"registry.compagny.com":{"password":"","username":""}}}` |
| `service.type`                   | Service Type                                     | `ClusterIP`                                                         |
| `service.targetPort`             | Service Port                                     | `80`                                                                |
| `service.protocol`               | Service Protocol                                 | `TCP`                                                               |
| `ingress.enabled`                | Expose application with ingress                  | `true`                                                              |
| `ingress.hostnames`              | Urls of exposed application                      | `['nexus.company.com']`                                  |
| `ingress.tls[hosts]`             | Array of TLS Hosts                               | `[]`                                                                |
| `ingress.tls[hosts[]]`           | Host name                                        | `['nexus.company.com']`                                  |
| `ingress.tls[hosts[secretName]]` | Secret for the current host name                 | `nexus`                                                  |
| `persistence.enabled`            | Enable persisting data on PVC                                        | `false`                                                             |
| `persistence.existingClaim`      | Does PVC already exist ?                                             | `false`                                                             |
| `persistence.size`               | PVC Size                                                             | `10Gi`                                                              |
| `persistence.storageClass`       | PVC storage class                                                    | `nil`                                                               |
| `persistence.accessMode`         | PVC Access Mode                                                      | `ReadWriteOnce`                                                     |
| `persistence.replicas`           | PVC storage class replicas (if possible)                             | `1`                                                                 |

## After Installing the Chart
After installing the chart a couple of actions need still to be done in order to use nexus. Please follow the instructions below.

### Nexus Configuration
The following steps need to be executed in order to use Nexus:

- [Configure Nexus](https://github.com/travelaudience/kubernetes-nexus/blob/master/docs/admin/configuring-nexus.md)
- [Configure Backups](https://github.com/travelaudience/kubernetes-nexus/blob/master/docs/admin/configuring-nexus.md#configure-backup)

and if GCP IAM authentication is enabled, please also check:
- [Enable GCP IAM authentication in Nexus ](https://github.com/travelaudience/kubernetes-nexus/blob/master/docs/admin/configuring-nexus-proxy.md#enable-gcp-iam-auth)

### Nexus Usage
To see how to use Nexus with different tools like Docker, Maven, Python, and so on please check:

- [Nexus Usage](https://github.com/travelaudience/kubernetes-nexus#usage)

### Disaster Recovery
In a disaster recovery scenario, the latest backup made by the nexus-backup container should be restored. In order to achieve this please follow the procedure described below:
- [Restore Backups](https://github.com/travelaudience/kubernetes-nexus#restore)
