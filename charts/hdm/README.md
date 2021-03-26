# HDM

## Configuration

The following table lists the configurable parameters of the chart and their default values.

| Parameter                        | Description                                      | Default                                                             |
|----------------------------------|--------------------------------------------------|---------------------------------------------------------------------|
| `image.replicaCount`             | Number of replicas to create                     | `1`                                                                 |
| `image.repository`               | Image repository.                                | `ghcr.io/curie-data-factory/hdm`                            |
| `image.tag`                      | Image Tag.                                       | `2.2.1`                                                             |
| `image.pullPolicy`               | Image pull policy.                               | `IfNotPresent`                                                      |
| `image.name`                     | Image name                                       | `hdm`                                                  |
| `image.deployRegistry`           | If the image is stored in a private registry     | `false`                                                             |
| `image.imagePullSecrets`         | Docker registry credentials Secret name          | `registrysecret`                                                    |
| `image.dataSecret`               | Secret storing docker image registry credentials | `{"auths":{"registry.compagny.com":{"password":"","username":""}}}` |
| `service.type`                   | Service Type                                     | `ClusterIP`                                                         |
| `service.targetPort`             | Service Port                                     | `80`                                                                |
| `service.protocol`               | Service Protocol                                 | `TCP`                                                               |
| `ingress.enabled`                | Expose application with ingress                  | `true`                                                              |
| `ingress.hostnames`              | Urls of exposed application                      | `['hdm.company.com']`                                  |
| `ingress.tls[hosts]`             | Array of TLS Hosts                               | `[]`                                                                |
| `ingress.tls[hosts[]]`           | Host name                                        | `['hdm.company.com']`                                  |
| `ingress.tls[hosts[secretName]]` | Secret for the current host name                 | `hdm`                                                  |
| `ldapConf.mountPath`             | Mount Path of ldap configmap on the container    | `/var/www/html/ldapconf/`                                           |
| `ldapConf.key`                   | Name of ldap config file                         | `conf.php`                                                          |
| `ldapConf.data`                  | Ldap credentials data                            | `nil`                                                               |
