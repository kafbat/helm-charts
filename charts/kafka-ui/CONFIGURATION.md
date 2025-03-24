## Parameters

### Common

| Name               | Description                                | Value |
| ------------------ | ------------------------------------------ | ----- |
| `replicaCount`     | Number of Kafka-UI replicas to deploy      | `1`   |
| `image.registry`   | image registry                             | `""`  |
| `image.repository` | image repository                           | `""`  |
| `image.pullPolicy` | image pull policy                          | `""`  |
| `image.tag`        | image tag (immutable tags are recommended) | `""`  |
| `imagePullSecrets` | Docker registry secret names as an array   | `[]`  |
| `nameOverride`     | String to partially override chart name    | `""`  |
| `fullnameOverride` | String to fully override app name          | `""`  |

### ServiceAccount configuration

| Name                         | Description                                          | Value  |
| ---------------------------- | ---------------------------------------------------- | ------ |
| `serviceAccount.name`        | The name of the ServiceAccount to use.               | `""`   |
| `serviceAccount.create`      | Specifies whether a ServiceAccount should be created | `true` |
| `serviceAccount.annotations` | Additional Service Account annotations               | `{}`   |

### Application configuration

| Name                             | Description                                                                                                                                        | Value |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| `existingConfigMap`              | Name of the existing ConfigMap with kafbat-ui environment variables                                                                                | `""`  |
| `yamlApplicationConfig`          | Kafbat-UI config in Yaml format                                                                                                                    | `{}`  |
| `yamlApplicationConfigConfigMap` | Map with name and keyName keys, name refers to the existing ConfigMap, keyName refers to the ConfigMap key with Kafbat-UI config in Yaml format    | `{}`  |
| `yamlApplicationConfigSecret`    | Secret with name and keyName keys, name refers to the existing ConfigMap, keyName refers to the ConfigMap key with Kafbat-UI config in Yaml format | `{}`  |
| `existingSecret`                 | Name of the existing Secret with Kafbat-UI environment variables                                                                                   | `""`  |
| `envs.secret`                    | Set of the sensitive environment variables to pass to Kafbat-UI                                                                                    | `{}`  |
| `envs.config`                    | Set of the environment variables to pass to Kafbat-UI                                                                                              | `{}`  |
| `envs.secretMappings`            | The mapping of existing secret to env variable.                                                                                                    | `{}`  |
| `envs.configMappings`            | The mapping of configmap and keyName to get env variable.                                                                                          | `{}`  |
| `env`                            | Envs to be added to the Kafka-UI container                                                                                                         | `{}`  |
| `resources`                      | Set Kafka-UI container requests and limits for different resources like CPU or memory (essential for production workloads)                         | `{}`  |
| `initContainers`                 | Add additional init containers to the Kafka-UI pods                                                                                                | `{}`  |
| `volumeMounts`                   | Optionally specify additional volumeMounts for the kafka-UI container                                                                              | `{}`  |
| `volumes`                        | Optionally specify additional volumes for the Kafka-UI pods                                                                                        | `{}`  |
| `hostAliases`                    | Kafka-UI pods host aliases                                                                                                                         | `{}`  |
| `extraContainers`                | Specify additional containers in extraContainers.                                                                                                  | `""`  |

### Network Policies

| Name                    | Description                                               | Value   |
| ----------------------- | --------------------------------------------------------- | ------- |
| `networkPolicy.enabled` | Specifies whether a NetworkPolicy should be created       | `false` |
| `podAnnotations`        | Annotations for Kafka-UI pods                             | `{}`    |
| `podLabels`             | Extra labels for Kafka-UI pods                            | `{}`    |
| `annotations`           | Annotations to be added to kafka-ui Deployment            | `{}`    |
| `labels`                | Labels to be added to kafka-ui Deployment                 | `{}`    |
| `probes.useHttpsScheme` | Set field schema as HTTPS for readines and liveness probe | `false` |

### Security Context

| Name                 | Description                                                                         | Value |
| -------------------- | ----------------------------------------------------------------------------------- | ----- |
| `podSecurityContext` | The security settings that you specify for a Pod apply to all Containers in the Pod | `{}`  |
| `securityContext`    | The security settings that you specify for a Kafka-UI container                     | `{}`  |

### Traffic Exposure Parameters

| Name                       | Description                                                                                                                      | Value       |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `service.type`             | Kafka-UI service type                                                                                                            | `ClusterIP` |
| `service.port`             | Kafka-UI service port number                                                                                                     | `80`        |
| `service.labels`           | Kafka-UI service labels                                                                                                          | `{}`        |
| `ingress.enabled`          | Enable ingress record generation for Kafka-UI                                                                                    | `""`        |
| `ingress.annotations`      | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations. | `{}`        |
| `ingress.labels`           | Labels for the Ingress                                                                                                           | `{}`        |
| `ingress.ingressClassName` | IngressClass that will be be used to implement the Ingress (Kubernetes 1.18+)                                                    | `""`        |
| `ingress.path`             | Default path for the ingress record                                                                                              | `/`         |
| `ingress.pathType`         | Ingress path type                                                                                                                | `Prefix`    |
| `ingress.host`             | Default hostname for the ingress record                                                                                          | `""`        |
| `ingress.tls.enabled`      | Enable TLS configuration for the host defined at `ingress.host` parameter                                                        | `false`     |
| `ingress.tls.secretName`   | The name of a pre-created Secret containing a TLS private key and certificate                                                    | `""`        |
| `ingress.precedingPaths`   | HTTP paths to add to the Ingress before the default path                                                                         | `[]`        |
| `ingress.succeedingPaths`  | Http paths to add to the Ingress after the default path                                                                          | `[]`        |
| `resources`                | Set Kafka-UI pod requests and limits for different resources like CPU or memory (essential for production workloads)             | `{}`        |

### Scheduling

| Name                   | Description                                                             | Value |
| ---------------------- | ----------------------------------------------------------------------- | ----- |
| `nodeSelector`         | Node labels for Kafka-UI pods assignment                                | `{}`  |
| `tolerations`          | Tolerations for Kafka-UI pods assignment                                | `[]`  |
| `affinity`             | Affinity for Kafka-UI pods assignment                                   | `{}`  |
| `revisionHistoryLimit` | Specify how many old ReplicaSets for this Deployment you want to retain | `nil` |
