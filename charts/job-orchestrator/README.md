# Job Orchestrator

[Job Orchestrator](https://github.com/curie-data-factory/job-orchestrator) Help Manages jobs by connecting Gitlab Runners / Nexus Ressources with Kubernetes.

## Installing the Chart

Before you can install the chart you will need to add the `curiedfcharts` repo to [Helm](https://helm.sh/).

```shell
helm repo add curiedfcharts https://curie-data-factory.github.io/helm-charts
helm repo update
```

After you've installed the repo you can install the chart.

```shell
helm upgrade --install --namespace default --values ./my-values.yaml my-release curiedfcharts/job-orchestrator
```

## Configuration

The following table lists the configurable parameters of the chart and their default values.

| Parameter                        | Description                                      | Default                                                             |
|----------------------------------|--------------------------------------------------|---------------------------------------------------------------------|
| `image.replicaCount`             | Number of replicas to create                     | `1`                                                                 |
| `image.repository`               | Image repository.                                | `ghcr.io/curie-data-factory/job-orchestrator`                            |
| `image.tag`                      | Image Tag.                                       | `1.3.2`                                                             |
| `image.pullPolicy`               | Image pull policy.                               | `IfNotPresent`                                                      |
| `image.name`                     | Image name                                       | `job-orchestrator`                                                  |
| `image.deployRegistry`           | If the image is stored in a private registry     | `false`                                                             |
| `image.imagePullSecrets`         | Docker registry credentials Secret name          | `registrysecret`                                                    |
| `image.dataSecret`               | Secret storing docker image registry credentials | `{"auths":{"registry.compagny.com":{"password":"","username":""}}}` |
| `service.type`                   | Service Type                                     | `ClusterIP`                                                         |
| `service.targetPort`             | Service Port                                     | `80`                                                                |
| `service.protocol`               | Service Protocol                                 | `TCP`                                                               |
| `ingress.enabled`                | Expose application with ingress                  | `true`                                                              |
| `ingress.hostnames`              | Urls of exposed application                      | `['job-orchestrator.company.com']`                                  |
| `ingress.tls[hosts]`             | Array of TLS Hosts                               | `[]`                                                                |
| `ingress.tls[hosts[]]`           | Host name                                        | `['job-orchestrator.company.com']`                                  |
| `ingress.tls[hosts[secretName]]` | Secret for the current host name                 | `job-orchestrator`                                                  |
| `configMap.mountPath`            | Mount Path of configmaps on the container        | `/var/www/html/conf/`                                               |
| `configMap.data`                 | Application Configmap data                       | `nil`                                                               |
| `configMap.cifs`                 | Cifs credentials configmap data                  | `nil`                                                               |
| `ldapConf.mountPath`             | Mount Path of ldap configmap on the container    | `/var/www/html/ldapconf/`                                           |
| `ldapConf.key`                   | Name of ldap config file                         | `conf.php`                                                          |
| `ldapConf.data`                  | Ldap credentials data                            | `nil`                                                               |
