# home-assistant

![Version: 2.0.0](https://img.shields.io/badge/Version-2.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2025.11.0](https://img.shields.io/badge/AppVersion-2025.11.0-informational?style=flat-square)

A Helm chart for Home Assistant on Kubernetes

## Chart Repo

Add the following repo to use the chart:

```console
helm repo add home-charts https://95gabor.github.io/home-charts
helm repo update
```

### Installation

- Install/upgrade in a namespace (using local chart directory):

```bash
helm upgrade --install home-assistant . \
  -n home-assistant --create-namespace \
  -f values.yaml
```

- Or install from a chart repository:

```bash
helm upgrade --install home-assistant home-charts/home-assistant \
  -n home-assistant --create-namespace \
  -f values.yaml
```

- Uninstall:

```bash
helm uninstall home-assistant -n home-assistant
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | See `values.yaml` | Affinity rules for pod scheduling |
| autoscaling | object | See `values.yaml` | Horizontal Pod Autoscaler configuration |
| autoscaling.enabled | bool | `false` | Enable horizontal pod autoscaling |
| autoscaling.maxReplicas | int | `100` | Maximum number of replicas |
| autoscaling.minReplicas | int | `1` | Minimum number of replicas |
| autoscaling.targetCPUUtilizationPercentage | int | `80` | Target CPU utilization percentage |
| certificate | object | See `values.yaml` | TLS certificate configuration via cert-manager |
| certificate.additionalHosts | list | `[]` | Additional hosts for the certificate |
| certificate.annotations | object | See `values.yaml` | Certificate annotations |
| certificate.domain | string | `"home.example.com"` | Domain name for the certificate |
| certificate.duration | string | empty | Certificate duration |
| certificate.enabled | bool | `false` | Enable certificate management |
| certificate.issuer | object | See `values.yaml` | Certificate issuer configuration |
| certificate.issuer.group | string | empty | Issuer group |
| certificate.issuer.kind | string | empty | Issuer kind |
| certificate.issuer.name | string | empty | Issuer name |
| certificate.privateKey | object | See `values.yaml` | Private key configuration |
| certificate.privateKey.algorithm | string | `"RSA"` | Private key algorithm |
| certificate.privateKey.encoding | string | `"PKCS1"` | Private key encoding |
| certificate.privateKey.rotationPolicy | string | `"Never"` | Private key rotation policy |
| certificate.privateKey.size | int | `2048` | Private key size |
| certificate.renewBefore | string | empty | Certificate renewal time before expiry |
| certificate.secretName | string | `"home-assistant-tls"` | Secret name for the TLS certificate |
| certificate.usages | list | `[]` | Certificate usages |
| container | object | See `values.yaml` | Container configuration |
| container.port | int | `8123` | Container port |
| env | list | `[]` | Environment variables |
| fullnameOverride | string | empty | Override the full name of the chart |
| homeAssistant | object | See `values.yaml` | Home Assistant specific configuration |
| homeAssistant.configurations | object | See `values.yaml` | Home Assistant configuration files |
| homeAssistant.configurations."configuration.yaml" | string | `"default_config:\n\ngroup: !include groups.yaml\nscript: !include scripts.yaml\nscene: !include scenes.yaml\n# automation: !include automations.yaml\n"` | Main configuration.yaml content |
| homeAssistant.configurations."groups.yaml" | string | `"# place your groups here\n"` | Groups configuration |
| homeAssistant.configurations."scenes.yaml" | string | `"# place your scenes here\n"` | Scenes configuration |
| homeAssistant.configurations."scripts.yaml" | string | `"# place your scripts here\n"` | Scripts configuration |
| homeAssistant.secrets | list | `[]` | Secrets configuration for Home Assistant |
| homeAssistant.timezone | string | `"Europe/Budapest"` | Timezone for Home Assistant |
| image | object | See `values.yaml` | Image configuration for Home Assistant |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"homeassistant/home-assistant"` | Home Assistant image repository |
| image.tag | string | empty | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | list | `[]` | Image pull secrets for private registries |
| ingress | object | See `values.yaml` | Ingress configuration |
| ingress.annotations | object | `{}` | Ingress annotations |
| ingress.className | string | empty | Ingress class name |
| ingress.enabled | bool | `false` | Enable ingress |
| ingress.hosts | list | `[{"host":"chart-example.local","paths":[{"path":"/","pathType":"ImplementationSpecific"}]}]` | Ingress hosts configuration |
| ingress.tls | list | `[]` | TLS configuration for ingress |
| nameOverride | string | empty | Override the name of the chart |
| nodeSelector | object | See `values.yaml` | Node selector for pod placement |
| persistence | object | See `values.yaml` | Persistence configuration |
| persistence.accessMode | string | `"ReadWriteOnce"` | Access mode for the persistent volume |
| persistence.size | string | `"4Gi"` | Size of the persistent volume |
| podAnnotations | object | See `values.yaml` | Pod annotations |
| podLabels | object | See `values.yaml` | Pod labels |
| podSecurityContext | object | See `values.yaml` | Pod security context |
| postgresOperator | object | See `values.yaml` | PostgreSQL operator configuration |
| postgresOperator.annotations | object | See `values.yaml` | Annotations for PostgreSQL resources |
| postgresOperator.databaseName | string | `"home-assistant"` | Database name |
| postgresOperator.dropOnDelete | bool | `false` | Drop database on delete |
| postgresOperator.enabled | bool | `false` | Enable PostgreSQL operator integration |
| postgresOperator.masterRole | string | `"home-assistant"` | Master role name |
| postgresOperator.privileges | string | `"OWNER"` | Database privileges |
| postgresOperator.role | string | `"home-assistant"` | Database role |
| postgresOperator.schema | string | `"home-assistant"` | Database schema |
| postgresOperator.secretName | string | `"home-assistant-database-credentials"` | Secret name for database credentials |
| replicaCount | int | `1` | Number of replicas for the Home Assistant deployment |
| resources | object | See `values.yaml` | Resource limits and requests |
| securityContext | object | See `values.yaml` | Security context for the container |
| service | object | See `values.yaml` | Service configuration |
| service.port | int | `80` | Service port |
| service.portName | string | `"http"` | Service port name |
| service.type | string | `"ClusterIP"` | Service type |
| serviceMonitor | object | See `values.yaml` | ServiceMonitor configuration for Prometheus |
| serviceMonitor.additionalLabels | object | See `values.yaml` | Additional labels for ServiceMonitor |
| serviceMonitor.annotations | object | See `values.yaml` | Annotations for ServiceMonitor |
| serviceMonitor.enabled | bool | `false` | Enable ServiceMonitor |
| serviceMonitor.interval | string | `"30s"` | Scrape interval |
| serviceMonitor.metricRelabelings | list | `[]` | Metric relabeling configuration |
| serviceMonitor.namespace | string | empty | Namespace for ServiceMonitor |
| serviceMonitor.relabelings | list | `[]` | Relabeling configuration |
| serviceMonitor.scheme | string | empty | Service scheme |
| serviceMonitor.scrapeTimeout | string | `"10s"` | Scrape timeout |
| serviceMonitor.selector | object | See `values.yaml` | Service selector |
| serviceMonitor.tlsConfig | object | See `values.yaml` | TLS configuration |
| tolerations | list | `[]` | Tolerations for pod scheduling |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
