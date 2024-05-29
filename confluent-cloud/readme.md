# Confluent Cloud OpenTelemetry metrics example

This example shows a setup for running a [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/) to scrape metrics from Confluent Cloud and post them to the New Relic OTLP Collector Endpoint.

This example also includes config for getting more Kafka metrics about brokers, topics and consumers using the OpenTelemetry Collector's `kafkametrics` receiver.

For more information, please see our [Kafka with Confluent documentation](https://docs.newrelic.com/docs/more-integrations/open-source-telemetry-integrations/opentelemetry/collector/collector-configuration-examples/opentelemetry-collector-kafka-confluentcloud/).

## Example setup options

There are 3 different examples here, Confluent on Docker, kubernetes, and kubernetes via helm. Follow the instructions below to run the example you're looking for.

## Running the docker compose example

### Docker ComposePrerequisites

1. You must have a Docker daemon running.
2. You must have [Docker compose](https://docs.docker.com/compose/) installed .
3. You must have a [Confluent Cloud account](https://www.confluent.io/get-started/) with a cluster running.

### Docker Compose Steps

First, set your environment variables in the `.env` file in this directory. For more information on the individual variables, reference the docs available below.

Once the variables are set, run the following command from the root directory to start the collector.

```shell
cd ./confluent-cloud/docker-compose

docker compose up
```

## Running the Helm example

### Helm Prerequisites

1. You must have a Kubernetes cluster running.
2. You must have [Helm](https://helm.sh/docs/intro/quickstart/) installed.
3. You must have a [Confluent Cloud account](https://www.confluent.io/get-started/) with a cluster running.

### Helm Steps

First, set your variables in the values file `./helm/values.yaml` in this directory. For more information on the individual variables, reference the docs available below.

Once the variables are set, run the following command from the root directory to install the collector in your Kubernetes cluster.

```shell
cd ./confluent-cloud/helm

helm install ./helm
```

## Running the raw k8s yaml example

### K8s Prerequisites

1. You must have a Kubernetes cluster running.
2. You must have a [Confluent Cloud account](https://www.confluent.io/get-started/) with a cluster running.

### K8s Steps

First, set your variables in the deployment file `./k8s/deployment.yaml` in this directory. For more information on the individual variables, reference the docs available below.

Once the variables are set, run the following command from the root directory to apply the collector to your Kubernetes cluster.

```shell
cd ./confluent-cloud/k8s

kubectl apply -f ./k8s
```

## Local Variable information

| Docker/K8s Variable | Helm Variable| Description | Docs |
| -------- | ----------- | ---- |
| **NEW_RELIC_API_KEY** | **newrelic.apiKey** |New Relic Ingest API Key |[API Key docs](https://docs.newrelic.com/docs/apis/intro-apis/new-relic-api-keys/) |
| **NEW_RELIC_OTLP_ENDPOINT** | **newrelic.otlpEndpoint** |Default US OTLP endpoint is <https://otlp.nr-data.net> | [OTLP endpoint config docs](https://docs.newrelic.com/docs/more-integrations/open-source-telemetry-integrations/opentelemetry/get-started/opentelemetry-set-up-your-app/#review-settings) |
| **CONFLUENT_API_KEY** | **confluent.apiKey** |API key for Confluent Cloud, can be created via cli by following the docs |[Confluent API key docs](https://docs.confluent.io/cloud/current/monitoring/metrics-api.html)|
| **CONFLUENT_API_SECRET** | **counfluent.apiSecret** | API secret for Confluent Cloud | [Confluent API key docs](https://docs.confluent.io/cloud/current/monitoring/metrics-api.html) |
| **CLUSTER_ID** | **confluent.clusterId** | ID of the cluster from Confluent Cloud | [List cluster ID docs](https://docs.confluent.io/confluent-cli/current/command-reference/kafka/cluster/confluent_kafka_cluster_list.html#description) |
| **CONNECTOR_ID** | **confluent.connectorId** |(Optional) ID of the connector from Confluent Cloud | [List connector ID docs](https://docs.confluent.io/confluent-cli/current/command-reference/connect/cluster/confluent_connect_cluster_list.html) |
| **SCHEMA_REGISTRY_ID** | **confluent.schemaRegistryId** |(Optional) ID of schema registry from Confluent Cloud | [List schema-registry ID docs](https://docs.confluent.io/confluent-cli/current/command-reference/schema-registry/schema/confluent_schema-registry_schema_list.html) |
| **CLUSTER_NAME** | **confluent.clusterName**     | Name of the cluster from Confluent Cloud                                  | [List cluster name docs](https://docs.confluent.io/confluent-cli/current/command-reference/kafka/cluster/confluent_kafka_cluster_list.html#description)                                   |
| **BOOTSTRAP_SERVER** | **confluent.bootstrapServer** | bootstrap server Endpoint for your cluster from Confluent Cloud           | [Describe cluster docs](https://docs.confluent.io/confluent-cli/current/command-reference/kafka/cluster/confluent_kafka_cluster_describe.html#description)|
