# samba

![Version: 2.0.0](https://img.shields.io/badge/Version-2.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: latest](https://img.shields.io/badge/AppVersion-latest-informational?style=flat-square)

A Helm chart for Samba Time Machine on Kubernetes

## Chart Repo

Add the following repo to use the chart:

```console
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
| affinity | object | See `values.yaml` | Affinity rules for pod scheduling |
| autoscaling | object | See `values.yaml` | Horizontal Pod Autoscaler configuration |
| autoscaling.enabled | bool | `false` | Enable horizontal pod autoscaling |
| autoscaling.maxReplicas | int | `100` | Maximum number of replicas |
| autoscaling.minReplicas | int | `1` | Minimum number of replicas |
| autoscaling.targetCPUUtilizationPercentage | int | `80` | Target CPU utilization percentage |
| dnsConfig | object | empty | DNS configuration for pods |
| dnsPolicy | string | "ClusterFirst" | DNS policy for pods |
| env | object | See `values.yaml` | Environment variables |
| env.ADVERTISED_HOSTNAME | string | empty | Advertised hostname for Time Machine |
| env.CUSTOM_SMB_CONF | string | `"false"` | Use custom SMB configuration |
| env.CUSTOM_USER | string | `"false"` | Use custom user configuration |
| env.DEBUG_LEVEL | string | `"1"` | Debug level (0-10) |
| env.EXTERNAL_CONF | string | empty | External configuration file path |
| env.HIDE_SHARES | string | `"no"` | Hide shares from network |
| env.MIMIC_MODEL | string | `"TimeCapsule8,119"` | Mimic Apple Time Capsule model |
| env.PASSWORD | string | `"timemachine"` | Password for Time Machine access (CHANGE THIS!) WARNING: This is a default password. You MUST change it in production! |
| env.SET_PERMISSIONS | string | `"false"` | Set permissions on volume |
| env.SHARE_NAME | string | `"TimeMachine"` | SMB share name |
| env.SMB_INHERIT_PERMISSIONS | string | `"no"` | Inherit permissions from volume |
| env.SMB_METADATA | string | `"stream"` | SMB metadata handling |
| env.SMB_NFS_ACES | string | `"no"` | Use NFS ACLs |
| env.SMB_PORT | string | `"445"` | SMB port |
| env.SMB_VFS_OBJECTS | string | `"fruit streams_xattr"` | SMB VFS objects |
| env.TM_GID | string | `"1000"` | Time Machine group ID |
| env.TM_GROUPNAME | string | `"timemachine"` | Time Machine group name |
| env.TM_UID | string | `"1000"` | Time Machine user ID |
| env.TM_USERNAME | string | `"timemachine"` | Time Machine username |
| env.VOLUME_SIZE_LIMIT | string | `"0"` | Volume size limit (0 = unlimited) |
| env.WORKGROUP | string | `"WORKGROUP"` | SMB workgroup name |
| envExtra | list | empty | Additional environment variables (for complex values like valueFrom) Use this for environment variables that need valueFrom or other complex structures |
| fullnameOverride | string | empty | Override the full name of the chart |
| hostNetwork | bool | `true` | Use host network for the pod |
| image | object | See `values.yaml` | Image configuration for Samba Time Machine |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"mbentley/timemachine"` | Samba Time Machine image repository |
| image.tag | string | empty | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | list | `[]` | Image pull secrets for private registries |
| nameOverride | string | empty | Override the name of the chart |
| networkPolicy | object | See `values.yaml` | Network Policy configuration |
| networkPolicy.egress | list | empty | Egress rules |
| networkPolicy.enabled | bool | `false` | Enable Network Policy |
| networkPolicy.ingress | list | empty | Ingress rules |
| nodeSelector | object | See `values.yaml` | Node selector for pod placement |
| persistence | object | See `values.yaml` | Persistence configuration |
| persistence.accessMode | string | `"ReadWriteOnce"` | Access mode for the persistent volume |
| persistence.size | string | `"500Gi"` | Size of the persistent volume |
| podAnnotations | object | See `values.yaml` | Pod annotations |
| podDisruptionBudget | object | See `values.yaml` | Pod Disruption Budget configuration |
| podDisruptionBudget.enabled | bool | `false` | Enable Pod Disruption Budget |
| podDisruptionBudget.maxUnavailable | string | empty | Maximum number of unavailable pods (mutually exclusive with minAvailable) |
| podDisruptionBudget.minAvailable | string | empty | Minimum number of available pods (mutually exclusive with maxUnavailable) |
| podLabels | object | See `values.yaml` | Pod labels |
| podSecurityContext | object | See `values.yaml` | Pod security context |
| replicaCount | int | `1` | Number of replicas for the Samba deployment |
| resources | object | See `values.yaml` | Resource limits and requests |
| resources.limits | object | `{"cpu":"500m","memory":"512Mi"}` | Resource limits |
| resources.requests | object | `{"cpu":"100m","memory":"128Mi"}` | Resource requests |
| securityContext | object | See `values.yaml` | Security context for the container |
| service | object | See `values.yaml` | Service configuration |
| service.ports | object | See `values.yaml` | Service ports configuration |
| service.ports.tcp139 | int | `139` | NetBIOS Name Service (TCP) |
| service.ports.tcp445 | int | `445` | SMB/CIFS (TCP) - Main file sharing port |
| service.ports.udp137 | int | `137` | NetBIOS Name Service (UDP) |
| service.ports.udp138 | int | `138` | NetBIOS Datagram Service (UDP) |
| service.type | string | `"ClusterIP"` | Service type |
| terminationGracePeriodSeconds | string | empty | Termination grace period in seconds |
| tolerations | list | `[]` | Tolerations for pod scheduling |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
