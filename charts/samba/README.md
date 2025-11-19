# samba

![Version: 3.0.2](https://img.shields.io/badge/Version-3.0.2-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: latest](https://img.shields.io/badge/AppVersion-latest-informational?style=flat-square)

A Helm chart for Samba Time Machine on Kubernetes

## Chart Repo

Add the following repo to use the chart:

```bash
helm repo add home-charts https://95gabor.github.io/home-charts
helm repo update
```

### Installation

- Install/upgrade in a namespace (using local chart directory):

```bash
helm upgrade --install samba . \
  -n samba --create-namespace \
  -f values.yaml
```

- Or install from a chart repository:

```bash
helm upgrade --install samba home-charts/samba \
  -n samba --create-namespace \
  -f values.yaml
```

- Uninstall:

```bash
helm uninstall samba -n samba
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
| dnsConfig | object | `{}` | DNS configuration for pods |
| dnsPolicy | string | `"ClusterFirst"` | DNS policy for pods |
| env | object | See `values.yaml` | Environment variables |
| env.ACCOUNT_timemachine | string | empty | Account username for Samba access Format: ACCOUNT_username (e.g., ACCOUNT_timemachine) |
| env.AVAHI_DISABLE | string | empty | Disable Avahi service (set to any value to disable) |
| env.AVAHI_NAME | string | empty | Avahi service name (default: hostname) |
| env.GID_timemachine | string | empty | Group ID for the account Format: GID_username (e.g., GID_timemachine) |
| env.MODEL | string | `"TimeCapsule"` | Time Machine model value for Avahi service Available options: TimeCapsule, Xserve, PowerBook, PowerMac, Macmini, iMac, MacBook, MacBookPro, MacBookAir, MacPro, MacPro6,1, MacPro7,1, etc. |
| env.NETBIOS_DISABLE | string | empty | Disable NetBIOS (set to any value to disable, not recommended) |
| env.PASSWORD_timemachine | string | `"timemachine"` | Password for the account (CHANGE THIS!) Format: PASSWORD_username (e.g., PASSWORD_timemachine) WARNING: This is a default password. You MUST change it in production! |
| env.SAMBA_CONF_LOG_LEVEL | string | `"1"` | Samba log level (default: 1) |
| env.SAMBA_CONF_MAP_TO_GUEST | string | `"Bad User"` | Samba map to guest setting |
| env.SAMBA_CONF_SERVER_ROLE | string | `"standalone server"` | Samba server role (default: standalone server) Note: $ is an invalid symbol in this env |
| env.SAMBA_CONF_SERVER_STRING | string | `"Samba Server"` | Samba server string |
| env.SAMBA_CONF_WORKGROUP | string | `"WORKGROUP"` | Samba workgroup name |
| env.SAMBA_VOLUME_CONFIG_timemachine | string | empty | Samba volume configuration Format: SAMBA_VOLUME_CONFIG_myconfigname For Time Machine, add: fruit:time machine = yes Use ; to separate multiple lines (automatically translated to \n) Example: path = /shares/timemachine; fruit:time machine = yes; fruit:time machine max size = 500G |
| env.UID_timemachine | string | empty | User ID for the account Format: UID_username (e.g., UID_timemachine) |
| env.WSDD2_DISABLE | string | empty | Disable wsdd2 service (set to any value to disable) |
| env.WSDD2_PARAMETERS | string | empty | wsdd2 parameters |
| envExtra | list | empty | Additional environment variables (for complex values like valueFrom) Use this for environment variables that need valueFrom or other complex structures Variables defined here will override variables with the same name from `env` |
| fullnameOverride | string | empty | Override the full name of the chart |
| hostNetwork | bool | `true` | Use host network for the pod |
| image | object | See `values.yaml` | Image configuration for Samba Time Machine |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy (IfNotPresent, Always, Never) |
| image.repository | string | `"ghcr.io/servercontainers/samba"` | Container image repository for Samba Time Machine |
| image.tag | string | empty | Container image tag (overrides chart appVersion if set) |
| imagePullSecrets | list | `[]` | Image pull secrets for private registries |
| nameOverride | string | empty | Override the name of the chart |
| networkPolicy | object | See `values.yaml` | Network Policy configuration |
| networkPolicy.egress | list | empty | Egress rules defining allowed outgoing traffic |
| networkPolicy.enabled | bool | `false` | Enable Network Policy to control network traffic to/from pods |
| networkPolicy.ingress | list | empty | Ingress rules defining allowed incoming traffic |
| nodeSelector | object | `{}` | Node selector for pod placement (constrain pods to specific nodes) |
| persistence | object | See `values.yaml` | Persistence configuration |
| persistence.accessMode | string | `"ReadWriteOnce"` | Access mode for the persistent volume (ReadWriteOnce, ReadWriteMany, ReadOnlyMany) |
| persistence.size | string | `"500Gi"` | Size of the persistent volume claim |
| persistence.storageClass | string | empty | Storage class for PVC (empty = use default storage class) |
| podAnnotations | object | `{}` | Pod annotations (metadata attached to pods) |
| podDisruptionBudget | object | See `values.yaml` | Pod Disruption Budget configuration |
| podDisruptionBudget.enabled | bool | `false` | Enable Pod Disruption Budget to control pod evictions during disruptions |
| podDisruptionBudget.maxUnavailable | string | empty | Maximum number of unavailable pods during disruptions (mutually exclusive with minAvailable) |
| podDisruptionBudget.minAvailable | string | empty | Minimum number of available pods during disruptions (mutually exclusive with maxUnavailable) |
| podLabels | object | `{}` | Pod labels (metadata for pod selection and organization) |
| podSecurityContext | object | `{}` | Pod security context (applies to all containers in the pod) |
| replicaCount | int | `1` | Number of replicas for the Samba deployment |
| resources | object | See `values.yaml` | Resource limits and requests |
| resources.limits | object | See `values.yaml` | Resource limits |
| resources.limits.cpu | string | `"500m"` | CPU limit for the container |
| resources.limits.memory | string | `"512Mi"` | Memory limit for the container |
| resources.requests | object | See `values.yaml` | Resource requests |
| resources.requests.cpu | string | `"100m"` | CPU request for the container |
| resources.requests.memory | string | `"128Mi"` | Memory request for the container |
| securityContext | object | `{}` | Security context for the container (applies to the main container) |
| service | object | See `values.yaml` | Service configuration |
| service.externalTrafficPolicy | string | empty | External traffic policy (Local, Cluster) - Only valid for LoadBalancer and NodePort services Preserves source IP address when set to Local. Requires health checks on all nodes. |
| service.ports | object | See `values.yaml` | Service ports configuration |
| service.ports.tcp139 | int | `139` | NetBIOS Name Service port (TCP) - Used for NetBIOS name resolution |
| service.ports.tcp445 | int | `445` | SMB/CIFS port (TCP) - Main file sharing port for SMB protocol |
| service.ports.udp137 | int | `137` | NetBIOS Name Service port (UDP) - Used for NetBIOS name resolution |
| service.ports.udp138 | int | `138` | NetBIOS Datagram Service port (UDP) - Used for NetBIOS datagram service |
| service.type | string | `"ClusterIP"` | Kubernetes service type (ClusterIP, NodePort, LoadBalancer) |
| terminationGracePeriodSeconds | string | empty | Termination grace period in seconds |
| tolerations | list | `[]` | Tolerations for pod scheduling (allow pods to be scheduled on tainted nodes) |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
