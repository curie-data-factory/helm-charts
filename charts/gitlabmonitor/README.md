# Gitlab Monitor

A web-based monitor dashboard for GitLab CI

To get more informations :

* [Github Source Code](https://github.com/timoschwarzer/gitlab-monitor)
* [Dockerhub Docker Image](https://hub.docker.com/r/timoschwarzer/gitlab-monitor)

## Prerequisites

1. Have a running [Kubernetes](https://kubernetes.io/docs/setup/) environment
2. Setup [Helm](https://github.com/kubernetes/helm)

## Installing the Chart

Before you can install the chart you will need to add the `curiedfcharts` repo to [Helm](https://helm.sh/).

```shell
helm repo add curiedfcharts https://curie-data-factory.github.io/helm-charts
helm repo update
```

After you've installed the repo you can install the chart.

```shell
helm upgrade --install --namespace default --values ./my-values.yaml my-release curiedfcharts/gitlab-monitor
```

## Configuration

The following table lists the configurable parameters of the chart and their default values.

`config` :

```yaml
config: |
  {
    "gitlabApi": "https://gitlab.example.com/api/v4",
    "privateToken": "ABCDEF123456",
    "maxAge": 168,
    "fetchCount": 20,
    "pipelinesOnly": false,
    "autoZoom": false,
    "showPipelineIds": true,
    "showJobs": "iconAndName",
    "showDurations": true,
    "showUsers": false,
    "projectVisibility": "any",
    "linkToFailureSound": null ,
    "title": null,
    "pollingIntervalMultiplier": 10,
    "filter": {
      "include": ".*",
      "includeTags": ".*",
      "exclude": null,
      "excludeTags": null
    },
    "projectFilter": {
      "*": {
        "include": ".*",
        "exclude": null,
        "default": null,
        "showMerged": false,
        "showTags": true,
        "maxPipelines": 10,
        "notifyFailureOn": null
      }
    }
  }
```

`resources` :

```yaml
resources:
  limits:
    cpu: 100m
    memory: 128Mi
  requests:
    cpu: 100m
    memory: 128Mi
```


| Parameter                        | Description                                      | Default                                                             |
|----------------------------------|--------------------------------------------------|---------------------------------------------------------------------|
| `image.replicaCount`             | Number of replicas to create                     | `1`                                                                 |
| `image.repository`               | Image repository.                                | `timoschwarzer/gitlab-monitor`                                      |
| `image.tag`                      | Image Tag.                                       | `latest`                                                            |
| `image.pullPolicy`               | Image pull policy.                               | `IfNotPresent`                                                      |
| `image.name`                     | Image name                                       | `gitlabmonitor`                                                     |
| `image.deployRegistry`           | If the image is stored in a private registry     | `false`                                                             |
| `image.imagePullSecrets`         | Docker registry credentials Secret name          | `registrysecret`                                                    |
| `image.dataSecret`               | Secret storing docker image registry credentials | `{"auths":{"registry.compagny.com":{"password":"","username":""}}}` |
| `service.type`                   | Service Type                                     | `ClusterIP`                                                         |
| `service.targetPort`             | Service Port                                     | `80`                                                                |
| `service.protocol`               | Service Protocol                                 | `TCP`                                                               |
| `ingress.enabled`                | Expose application with ingress                  | `true`                                                              |
| `ingress.hostnames`              | Urls of exposed application                      | `['gitlabmonitor.company.com']`                                     |
| `ingress.tls`                    | Array of TLS Hosts                               | `[]`                                                                |
| `ingress.tls[hosts]`             | Host name                                        | `['gitlabmonitor.company.com']`                                     |
| `ingress.tls[hosts[secretName]]` | Secret for the current host name                 | `gitlabmonitor`                                                     |
| `resources`                      | Resources requirements & limits                  | `See values.yaml`                                                   |
| `config`                         | Config values for Gitlab Monitor                 | `See values.yaml`                                                   |
