# home-assistant

![GitHub Release](https://img.shields.io/github/v/release/95gabor/home-charts?style=flat-square&filter=home-assistant-*) ![Chart Type](https://img.shields.io/badge/dynamic/yaml?style=flat-square&url=https%3A%2F%2Fraw.githubusercontent.com%2F95gabor%2Fhome-charts%2Fmain%2Fcharts%2Fhome-assistant%2FChart.yaml&query=%24.type&label=Type) ![App Version](https://img.shields.io/badge/dynamic/yaml?style=flat-square&url=https%3A%2F%2Fraw.githubusercontent.com%2F95gabor%2Fhome-charts%2Fmain%2Fcharts%2Fhome-assistant%2FChart.yaml&query=%24.appVersion&label=AppVersion)

Home Assistant Helm chart for Kubernetes

## Usage

```sh
helm repo add home-charts https://95gabor.github.io/home-charts
helm install home-assistant home-charts/home-assistant
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| certificate.additionalHosts | list | `[]` |  |
| certificate.annotations | object | `{}` |  |
| certificate.domain | string | `"home.example.com"` |  |
| certificate.duration | string | `""` |  |
| certificate.enabled | bool | `false` |  |
| certificate.issuer.group | string | `""` |  |
| certificate.issuer.kind | string | `""` |  |
| certificate.issuer.name | string | `""` |  |
| certificate.privateKey.algorithm | string | `"RSA"` |  |
| certificate.privateKey.encoding | string | `"PKCS1"` |  |
| certificate.privateKey.rotationPolicy | string | `"Never"` |  |
| certificate.privateKey.size | int | `2048` |  |
| certificate.renewBefore | string | `""` |  |
| certificate.secretName | string | `"home-assistant-tls"` |  |
| certificate.usages | list | `[]` |  |
| container.port | int | `8123` |  |
| env | list | `[]` |  |
| fullnameOverride | string | `""` |  |
| homeAssistant.configurations."configuration.yaml" | string | `"default_config:\n\ngroup: !include groups.yaml\nscript: !include scripts.yaml\nscene: !include scenes.yaml\n# automation: !include automations.yaml\n"` |  |
| homeAssistant.configurations."groups.yaml" | string | `"# place your groups here\n"` |  |
| homeAssistant.configurations."scenes.yaml" | string | `"# place your scenes here\n"` |  |
| homeAssistant.configurations."scripts.yaml" | string | `"# place your scripts here\n"` |  |
| homeAssistant.secrets | list | `[]` |  |
| homeAssistant.timezone | string | `"Europe/Budapest"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"homeassistant/home-assistant"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.className | string | `""` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| persistence.accessMode | string | `"ReadWriteOnce"` |  |
| persistence.size | string | `"4Gi"` |  |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| postgresOperator.annotations | object | `{}` |  |
| postgresOperator.databaseName | string | `"home-assistant"` |  |
| postgresOperator.dropOnDelete | bool | `false` |  |
| postgresOperator.enabled | bool | `false` |  |
| postgresOperator.masterRole | string | `"home-assistant"` |  |
| postgresOperator.privileges | string | `"OWNER"` |  |
| postgresOperator.role | string | `"home-assistant"` |  |
| postgresOperator.schema | string | `"home-assistant"` |  |
| postgresOperator.secretName | string | `"home-assistant-database-credentials"` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.port | int | `80` |  |
| service.portName | string | `"http"` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceMonitor.additionalLabels | object | `{}` |  |
| serviceMonitor.annotations | object | `{}` |  |
| serviceMonitor.enabled | bool | `false` |  |
| serviceMonitor.interval | string | `"30s"` |  |
| serviceMonitor.metricRelabelings | list | `[]` |  |
| serviceMonitor.namespace | string | `""` |  |
| serviceMonitor.relabelings | list | `[]` |  |
| serviceMonitor.scheme | string | `""` |  |
| serviceMonitor.scrapeTimeout | string | `"10s"` |  |
| serviceMonitor.selector | object | `{}` |  |
| serviceMonitor.tlsConfig | object | `{}` |  |
| tolerations | list | `[]` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.12.0](https://github.com/norwoodj/helm-docs/releases/v1.12.0)
