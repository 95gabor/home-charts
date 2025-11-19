# home-assistant

![Version: 2.3.0](https://img.shields.io/badge/Version-2.3.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2025.11.2](https://img.shields.io/badge/AppVersion-2025.11.2-informational?style=flat-square)

A Helm chart for Home Assistant on Kubernetes

## Chart Repo

Add the following repo to use the chart:

```bash
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
| affinity | object | `{}` | Affinity rules for pod scheduling (pod affinity/anti-affinity, node affinity) |
| autoscaling | object | See `values.yaml` | Horizontal Pod Autoscaler configuration |
| autoscaling.enabled | bool | `false` | Enable Horizontal Pod Autoscaler to automatically scale pods based on metrics |
| autoscaling.maxReplicas | int | `100` | Maximum number of pod replicas allowed |
| autoscaling.minReplicas | int | `1` | Minimum number of pod replicas to maintain |
| autoscaling.targetCPUUtilizationPercentage | int | `80` | Target CPU utilization percentage for autoscaling (0-100) |
| certificate | object | See `values.yaml` | TLS certificate configuration via cert-manager |
| certificate.additionalHosts | list | `[]` | Additional hostnames to include in the certificate (SAN entries) |
| certificate.annotations | object | `{}` | Annotations to add to the Certificate resource |
| certificate.domain | string | `"home.example.com"` | Primary domain name for the TLS certificate |
| certificate.duration | string | empty | Certificate validity duration (e.g., "2160h" for 90 days) |
| certificate.enabled | bool | `false` | Enable automatic TLS certificate management using cert-manager |
| certificate.issuer | object | See `values.yaml` | Certificate issuer configuration |
| certificate.issuer.group | string | empty | API group of the issuer resource (e.g., "cert-manager.io") |
| certificate.issuer.kind | string | empty | Kind of the issuer resource (Issuer or ClusterIssuer) |
| certificate.issuer.name | string | empty | Name of the issuer resource |
| certificate.privateKey | object | See `values.yaml` | Private key configuration |
| certificate.privateKey.algorithm | string | `"RSA"` | Private key algorithm (RSA or ECDSA) |
| certificate.privateKey.encoding | string | `"PKCS1"` | Private key encoding format (PKCS1 or PKCS8) |
| certificate.privateKey.rotationPolicy | string | `"Never"` | Private key rotation policy (Never, Always, OnKeyRotation) |
| certificate.privateKey.size | int | `2048` | Private key size in bits (for RSA: 2048, 4096; for ECDSA: 256, 384, 521) |
| certificate.renewBefore | string | empty | Time before certificate expiry to start renewal (e.g., "720h" for 30 days) |
| certificate.secretName | string | `"home-assistant-tls"` | Kubernetes secret name where the TLS certificate will be stored |
| certificate.usages | list | `[]` | Certificate key usages (e.g., ["signing", "key encipherment", "server auth"]) |
| container | object | See `values.yaml` | Container configuration |
| container.port | int | `8123` | Port number the container listens on |
| dnsConfig | object | `{}` | DNS configuration for pods |
| dnsPolicy | string | "ClusterFirst" | DNS policy for pods |
| env | list | `[]` | Environment variables |
| fullnameOverride | string | empty | Override the full name of the chart |
| homeAssistant | object | See `values.yaml` | Home Assistant specific configuration |
| homeAssistant.configurations | object | See `values.yaml` | Home Assistant configuration files (mounted as ConfigMap) |
| homeAssistant.configurations."configuration.yaml" | string | See `values.yaml` | Main configuration.yaml content |
| homeAssistant.configurations."groups.yaml" | string | See `values.yaml` | Groups configuration |
| homeAssistant.configurations."scenes.yaml" | string | See `values.yaml` | Scenes configuration |
| homeAssistant.configurations."scripts.yaml" | string | See `values.yaml` | Scripts configuration |
| homeAssistant.secrets | list | `[]` | Secrets configuration for Home Assistant |
| homeAssistant.timezone | string | `"Europe/Budapest"` | Timezone for Home Assistant (IANA timezone database name) |
| image | object | See `values.yaml` | Image configuration for Home Assistant |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy (IfNotPresent, Always, Never) |
| image.repository | string | `"homeassistant/home-assistant"` | Container image repository for Home Assistant |
| image.tag | string | empty | Container image tag (overrides chart appVersion if set) |
| imagePullSecrets | list | `[]` | Image pull secrets for private registries |
| ingress | object | See `values.yaml` | Ingress configuration |
| ingress.annotations | object | `{}` | Ingress annotations (e.g., for cert-manager, nginx settings) |
| ingress.className | string | empty | Ingress class name (e.g., nginx, traefik) |
| ingress.enabled | bool | `false` | Enable ingress resource creation |
| ingress.hosts | list | `[]` | Ingress hosts configuration Each host can be configured with a single path (using 'path' and 'pathType') or multiple paths (using 'paths' array). If 'paths' is specified, it takes precedence. |
| ingress.tls | list | `[]` | TLS configuration for ingress (certificate secrets) |
| nameOverride | string | empty | Override the name of the chart |
| networkPolicy | object | See `values.yaml` | Network Policy configuration |
| networkPolicy.egress | list | empty | Egress rules defining allowed outgoing traffic |
| networkPolicy.enabled | bool | `false` | Enable Network Policy to control network traffic to/from pods |
| networkPolicy.ingress | list | empty | Ingress rules defining allowed incoming traffic |
| nodeSelector | object | `{}` | Node selector for pod placement (constrain pods to specific nodes) |
| persistence | object | See `values.yaml` | Persistence configuration |
| persistence.accessMode | string | `"ReadWriteOnce"` | Access mode for the persistent volume (ReadWriteOnce, ReadWriteMany, ReadOnlyMany) |
| persistence.size | string | `"4Gi"` | Size of the persistent volume claim |
| persistence.storageClass | string | empty | Storage class for PVC (empty = use default storage class) |
| podAnnotations | object | `{}` | Pod annotations (metadata attached to pods) |
| podDisruptionBudget | object | See `values.yaml` | Pod Disruption Budget configuration |
| podDisruptionBudget.enabled | bool | `false` | Enable Pod Disruption Budget to control pod evictions during disruptions |
| podDisruptionBudget.maxUnavailable | string | empty | Maximum number of unavailable pods during disruptions (mutually exclusive with minAvailable) |
| podDisruptionBudget.minAvailable | string | empty | Minimum number of available pods during disruptions (mutually exclusive with maxUnavailable) |
| podLabels | object | `{}` | Pod labels (metadata for pod selection and organization) |
| podSecurityContext | object | `{}` | Pod security context (applies to all containers in the pod) |
| postgresOperator | object | See `values.yaml` | PostgreSQL operator configuration |
| postgresOperator.annotations | object | `{}` | Annotations to add to PostgreSQL resources created by the operator |
| postgresOperator.databaseName | string | `"home-assistant"` | Name of the PostgreSQL database to create |
| postgresOperator.dropOnDelete | bool | `false` | Whether to drop the database when the resource is deleted |
| postgresOperator.enabled | bool | `false` | Enable PostgreSQL operator integration for automatic database provisioning |
| postgresOperator.masterRole | string | `"home-assistant"` | Master role name for the database |
| postgresOperator.privileges | string | `"OWNER"` | Database privileges granted to the role (OWNER, READ, WRITE) |
| postgresOperator.role | string | `"home-assistant"` | Database role name for application access |
| postgresOperator.schema | string | `"home-assistant"` | Database schema name |
| postgresOperator.secretName | string | `"home-assistant-database-credentials"` | Kubernetes secret name where database credentials will be stored |
| replicaCount | int | `1` | Number of replicas for the Home Assistant deployment |
| resources | object | See `values.yaml` | Resource limits and requests |
| resources.limits | object | See `values.yaml` | Resource limits |
| resources.limits.cpu | string | `"2000m"` | CPU limit for the container |
| resources.limits.memory | string | `"2Gi"` | Memory limit for the container |
| resources.requests | object | See `values.yaml` | Resource requests |
| resources.requests.cpu | string | `"500m"` | CPU request for the container |
| resources.requests.memory | string | `"512Mi"` | Memory request for the container |
| securityContext | object | See `values.yaml` | Security context for the container (applies to the main container) |
| securityContext.capabilities | object | See `values.yaml` | Linux capabilities to add to the container NET_ADMIN and NET_RAW are required for Home Assistant to manage network interfaces (e.g., for Z-Wave, Zigbee, and other network-based integrations) |
| securityContext.capabilities.add | list | `["NET_ADMIN","NET_RAW"]` | Capabilities to add |
| service | object | See `values.yaml` | Service configuration |
| service.port | int | `80` | Service port number exposed by the service |
| service.portName | string | `"http"` | Name of the service port |
| service.type | string | `"ClusterIP"` | Kubernetes service type (ClusterIP, NodePort, LoadBalancer) |
| serviceMonitor | object | See `values.yaml` | ServiceMonitor configuration for Prometheus |
| serviceMonitor.additionalLabels | object | `{}` | Additional labels to add to the ServiceMonitor |
| serviceMonitor.annotations | object | `{}` | Annotations to add to the ServiceMonitor |
| serviceMonitor.enabled | bool | `false` | Enable ServiceMonitor resource for Prometheus Operator |
| serviceMonitor.interval | string | `"30s"` | Interval at which Prometheus should scrape metrics |
| serviceMonitor.metricRelabelings | list | `[]` | Metric relabeling rules applied after scraping |
| serviceMonitor.namespace | string | empty | Namespace where the ServiceMonitor should be created |
| serviceMonitor.relabelings | list | `[]` | Relabeling rules applied before scraping |
| serviceMonitor.scheme | string | empty | Protocol scheme for scraping (http or https) |
| serviceMonitor.scrapeTimeout | string | `"10s"` | Timeout for metric scraping |
| serviceMonitor.selector | object | `{}` | Service selector to match the service |
| serviceMonitor.tlsConfig | object | `{}` | TLS configuration for secure scraping |
| terminationGracePeriodSeconds | string | empty | Termination grace period in seconds |
| tolerations | list | `[]` | Tolerations for pod scheduling (allow pods to be scheduled on tainted nodes) |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
