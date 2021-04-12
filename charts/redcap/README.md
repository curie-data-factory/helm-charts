# Redcap

[Redcap](https://www.project-redcap.org/) REDCap is a secure web application for building and managing online surveys and databases.

This chart use a specific image definition available here : [https://github.com/curie-data-factory/redcap](https://github.com/curie-data-factory/redcap)

## Installing the Chart

Before you can install the chart you will need to add the `curiedfcharts` repo to [Helm](https://helm.sh/).

```shell
helm repo add curiedfcharts https://curie-data-factory.github.io/helm-charts
helm repo update
```

After you've installed the repo you can install the chart.

```shell
helm upgrade --install --namespace default --values ./my-values.yaml my-release curiedfcharts/redcap
```

## Configuration

The following table lists the configurable parameters of the chart and their default values.


| Parameter                        | Description                                      | Default                                                             |
|----------------------------------|--------------------------------------------------|---------------------------------------------------------------------|
| `image.replicaCount`             | Number of replicas to create                     | `1`                                                                 |
| `image.repository`               | Image repository.                                | `registry.compagny.com/redcap`                                      |
| `image.tag`                      | Image Tag.                                       | `1.3.0`                                                             |
| `image.pullPolicy`               | Image pull policy.                               | `IfNotPresent`                                                      |
| `image.name`                     | Image name                                       | `redcap`                                                            |
| `image.deployRegistry`           | If the image is stored in a private registry     | `false`                                                             |
| `image.imagePullSecrets`         | Docker registry credentials Secret name          | `registrysecret`                                                    |
| `image.dataSecret`               | Secret storing docker image registry credentials | `{"auths":{"registry.compagny.com":{"password":"","username":""}}}` |
| `livenesscheck`                  | Enable Liveness check                            | `true`                                                              |
| `service.type`                   | Service Type                                     | `ClusterIP`                                                         |
| `service.targetPort`             | Service Port                                     | `80`                                                                |
| `service.protocol`               | Service Protocol                                 | `TCP`                                                               |
| `ingress.enabled`                | Expose application with ingress                  | `true`                                                              |
| `ingress.hostnames`              | Urls of exposed application                      | `['redcap.company.com']`                                            |
| `ingress.tls`                    | Array of TLS Hosts                               | `[]`                                                                |
| `ingress.tls[hosts]`             | Host name                                        | `['redcap.company.com']`                                            |
| `ingress.tls[hosts[secretName]]` | Secret for the current host name                 | `redcap`                                                            |
| `persistence.enabled`            | Enable persisting data on PVC                    | `false`                                                             |
| `persistence.existingClaim`      | Does PVC already exist ?                         | `false`                                                             |
| `persistence.size`               | PVC Size                                         | `50Gi`                                                              |
| `persistence.storageClass`       | PVC storage class                                | `nil`                                                               |
| `persistence.accessMode`         | PVC Access Mode                                  | `ReadWriteOnce`                                                     |
| `persistence.replicas`           | PVC storage class replicas (if possible)         | `1`                                                                 |
| `persistence.volumeName`         | Directory name                                   | `edocs`                                                             |
| `persistence.mountPath`          | Directory mount path                             | `/var/www/site/edocs`                                               |
| `CRON_TASK_SCHEDULE`             | Redcap CRON Task Schedule                        | `0 * * * *`                                                         |
| `DB_HOSTNAME`                    | Redcap DB Hostname                               | `nil`                                                               |
| `DB_NAME`                        | Redcap DB Name                                   | `nil`                                                               |
| `DB_USERNAME`                    | Redcap DB Username                               | `nil`                                                               |
| `DB_PASSWORD`                    | Redcap DB Password                               | `nil`                                                               |
| `SMB_MOUNT_ENABLED`              | Redcap Mount docs directory to Network Share     | `true`                                                              |
| `SMB_USER`                       | Network Share Username                           | `nil`                                                               |
| `SMB_PASSWORD`                   | Network Share Password                           | `nil`                                                               |
| `SMB_SOURCEPATH`                 | Network Share Source Path                        | `nil`                                                               |
| `SMB_DESTPATH`                   | Network Share Destination Path                   | `nil`                                                               |
| `SMB_DOMAIN`                     | Network Share Domain                             | `nil`                                                               |
| `SALT`                           | Network Share SALT                               | `nil`                                                               |
| `LDAP`                           | Redcap LDAP Auth configuration data              | `nil`                                                               |
