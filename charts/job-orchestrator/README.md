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

The following table lists the configurable parameters of the _job-orchestrator_ chart and their default values.

| Parameter          	| Description                  	| Default                                  	|
|--------------------	|------------------------------	|------------------------------------------	|
| `replicaCount`     	| Number of replicas to create 	| `1`                                      	|
| `image.repository` 	| Image repository.            	| `registry.compagny.com/job-orchestrator` 	|
| `image.tag`        	| Image Tag.                   	| `1.3.0`                                  	|
| `image.pullPolicy` 	| Image pull policy.           	| `IfNotPresent`                           	|
| `image.name`       	| Image name                   	| `job-orchestrator`                       	|
