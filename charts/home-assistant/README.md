# home-assistant

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2025.10.4](https://img.shields.io/badge/AppVersion-2025.10.4-informational?style=flat-square)

A Helm chart for Home Assistant on Kubernetes

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Affinity rules for pod scheduling |
| autoscaling | object | `{"enabled":false,"maxReplicas":100,"minReplicas":1,"targetCPUUtilizationPercentage":80}` | Horizontal Pod Autoscaler configuration |
| autoscaling.enabled | bool | `false` | Enable horizontal pod autoscaling |
| autoscaling.maxReplicas | int | `100` | Maximum number of replicas |
| autoscaling.minReplicas | int | `1` | Minimum number of replicas |
| autoscaling.targetCPUUtilizationPercentage | int | `80` | Target CPU utilization percentage |
| certificate | object | `{"additionalHosts":[],"annotations":{},"domain":"home.example.com","duration":"","enabled":false,"issuer":{"group":"","kind":"","name":""},"privateKey":{"algorithm":"RSA","encoding":"PKCS1","rotationPolicy":"Never","size":2048},"renewBefore":"","secretName":"home-assistant-tls","usages":[]}` | TLS certificate configuration via cert-manager |
| certificate.additionalHosts | list | `[]` | Additional hosts for the certificate |
| certificate.annotations | object | `{}` | Certificate annotations |
| certificate.domain | string | `"home.example.com"` | Domain name for the certificate |
| certificate.duration | string | `""` | Certificate duration |
| certificate.enabled | bool | `false` | Enable certificate management |
| certificate.issuer | object | `{"group":"","kind":"","name":""}` | Certificate issuer configuration |
| certificate.issuer.group | string | `""` | Issuer group |
| certificate.issuer.kind | string | `""` | Issuer kind |
| certificate.issuer.name | string | `""` | Issuer name |
| certificate.privateKey | object | `{"algorithm":"RSA","encoding":"PKCS1","rotationPolicy":"Never","size":2048}` | Private key configuration |
| certificate.privateKey.algorithm | string | `"RSA"` | Private key algorithm |
| certificate.privateKey.encoding | string | `"PKCS1"` | Private key encoding |
| certificate.privateKey.rotationPolicy | string | `"Never"` | Private key rotation policy |
| certificate.privateKey.size | int | `2048` | Private key size |
| certificate.renewBefore | string | `""` | Certificate renewal time before expiry |
| certificate.secretName | string | `"home-assistant-tls"` | Secret name for the TLS certificate |
| certificate.usages | list | `[]` | Certificate usages |
| container | object | `{"port":8123}` | Container configuration |
| container.port | int | `8123` | Container port |
| env | list | `[]` | Environment variables |
| fullnameOverride | string | `""` | Override the full name of the chart |
| homeAssistant | object | `{"configurations":{"configuration.yaml":"default_config:\n\ngroup: !include groups.yaml\nscript: !include scripts.yaml\nscene: !include scenes.yaml\n# automation: !include automations.yaml\n","groups.yaml":"# place your groups here\n","scenes.yaml":"# place your scenes here\n","scripts.yaml":"# place your scripts here\n"},"secrets":[],"timezone":"Europe/Budapest"}` | Home Assistant specific configuration |
| homeAssistant.configurations | object | `{"configuration.yaml":"default_config:\n\ngroup: !include groups.yaml\nscript: !include scripts.yaml\nscene: !include scenes.yaml\n# automation: !include automations.yaml\n","groups.yaml":"# place your groups here\n","scenes.yaml":"# place your scenes here\n","scripts.yaml":"# place your scripts here\n"}` | Home Assistant configuration files |
| homeAssistant.configurations."configuration.yaml" | string | `"default_config:\n\ngroup: !include groups.yaml\nscript: !include scripts.yaml\nscene: !include scenes.yaml\n# automation: !include automations.yaml\n"` | Main configuration.yaml content |
| homeAssistant.configurations."groups.yaml" | string | `"# place your groups here\n"` | Groups configuration |
| homeAssistant.configurations."scenes.yaml" | string | `"# place your scenes here\n"` | Scenes configuration |
| homeAssistant.configurations."scripts.yaml" | string | `"# place your scripts here\n"` | Scripts configuration |
| homeAssistant.secrets | list | `[]` | Secrets configuration for Home Assistant |
| homeAssistant.timezone | string | `"Europe/Budapest"` | Timezone for Home Assistant |
| image | object | `{"pullPolicy":"IfNotPresent","repository":"homeassistant/home-assistant","tag":""}` | Image configuration for Home Assistant |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"homeassistant/home-assistant"` | Home Assistant image repository |
| image.tag | string | `""` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | list | `[]` | Image pull secrets for private registries |
| ingress | object | `{"annotations":{},"className":"","enabled":false,"hosts":[{"host":"chart-example.local","paths":[{"path":"/","pathType":"ImplementationSpecific"}]}],"tls":[]}` | Ingress configuration |
| ingress.annotations | object | `{}` | Ingress annotations |
| ingress.className | string | `""` | Ingress class name |
| ingress.enabled | bool | `false` | Enable ingress |
| ingress.hosts | list | `[{"host":"chart-example.local","paths":[{"path":"/","pathType":"ImplementationSpecific"}]}]` | Ingress hosts configuration |
| ingress.tls | list | `[]` | TLS configuration for ingress |
| nameOverride | string | `""` | Override the name of the chart |
| nodeSelector | object | `{}` | Node selector for pod placement |
| persistence | object | `{"accessMode":"ReadWriteOnce","size":"4Gi"}` | Persistence configuration |
| persistence.accessMode | string | `"ReadWriteOnce"` | Access mode for the persistent volume |
| persistence.size | string | `"4Gi"` | Size of the persistent volume |
| podAnnotations | object | `{}` | Pod annotations |
| podLabels | object | `{}` | Pod labels |
| podSecurityContext | object | `{}` | Pod security context |
| postgresOperator | object | `{"annotations":{},"databaseName":"home-assistant","dropOnDelete":false,"enabled":false,"masterRole":"home-assistant","privileges":"OWNER","role":"home-assistant","schema":"home-assistant","secretName":"home-assistant-database-credentials"}` | PostgreSQL operator configuration |
| postgresOperator.annotations | object | `{}` | Annotations for PostgreSQL resources |
| postgresOperator.databaseName | string | `"home-assistant"` | Database name |
| postgresOperator.dropOnDelete | bool | `false` | Drop database on delete |
| postgresOperator.enabled | bool | `false` | Enable PostgreSQL operator integration |
| postgresOperator.masterRole | string | `"home-assistant"` | Master role name |
| postgresOperator.privileges | string | `"OWNER"` | Database privileges |
| postgresOperator.role | string | `"home-assistant"` | Database role |
| postgresOperator.schema | string | `"home-assistant"` | Database schema |
| postgresOperator.secretName | string | `"home-assistant-database-credentials"` | Secret name for database credentials |
| replicaCount | int | `1` | Number of replicas for the Home Assistant deployment |
| resources | object | `{}` | Resource limits and requests |
| securityContext | object | `{}` | Security context for the container |
| service | object | `{"port":80,"portName":"http","type":"ClusterIP"}` | Service configuration |
| service.port | int | `80` | Service port |
| service.portName | string | `"http"` | Service port name |
| service.type | string | `"ClusterIP"` | Service type |
| serviceMonitor | object | `{"additionalLabels":{},"annotations":{},"enabled":false,"interval":"30s","metricRelabelings":[],"namespace":"","relabelings":[],"scheme":"","scrapeTimeout":"10s","selector":{},"tlsConfig":{}}` | ServiceMonitor configuration for Prometheus |
| serviceMonitor.additionalLabels | object | `{}` | Additional labels for ServiceMonitor |
| serviceMonitor.annotations | object | `{}` | Annotations for ServiceMonitor |
| serviceMonitor.enabled | bool | `false` | Enable ServiceMonitor |
| serviceMonitor.interval | string | `"30s"` | Scrape interval |
| serviceMonitor.metricRelabelings | list | `[]` | Metric relabeling configuration |
| serviceMonitor.namespace | string | `""` | Namespace for ServiceMonitor |
| serviceMonitor.relabelings | list | `[]` | Relabeling configuration |
| serviceMonitor.scheme | string | `""` | Service scheme |
| serviceMonitor.scrapeTimeout | string | `"10s"` | Scrape timeout |
| serviceMonitor.selector | object | `{}` | Service selector |
| serviceMonitor.tlsConfig | object | `{}` | TLS configuration |
| tolerations | list | `[]` | Tolerations for pod scheduling |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
