# mlp

![Version: 0.5.1](https://img.shields.io/badge/Version-0.5.1-informational?style=flat-square) ![AppVersion: v1.7.4-build.6-322163a](https://img.shields.io/badge/AppVersion-v1.7.4--build.6--322163a-informational?style=flat-square)

MLP API

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| caraml-dev | <caraml-dev@caraml.dev> |  |

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://caraml-dev.github.io/helm-charts | common | 0.2.8 |
| https://charts.helm.sh/stable | postgresql | 7.0.2 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| caramlEnvironments.enabled | bool | `true` |  |
| caramlEnvironments.environmentConfigs | object | `{}` |  |
| caramlEnvironments.imageBuilderConfigs | string | `""` |  |
| config.apiHost | string | `"http://mlp/v1"` |  |
| config.applications | list | `[{"configuration":{"api":"/api/merlin/v1","iconName":"machineLearningApp","navigation":[{"destination":"/models","label":"Models"},{"destination":"/transformer-simulator","label":"Transformer Simulator"}]},"description":"Platform for deploying machine learning models","homepage":"/merlin","name":"Merlin"},{"configuration":{"api":"/api/turing/v1","iconName":"graphApp","navigation":[{"destination":"/routers","label":"Routers"},{"destination":"/ensemblers","label":"Ensemblers"},{"destination":"/jobs","label":"Ensembling Jobs"},{"destination":"/experiments","label":"Experiments"}]},"description":"Platform for setting up ML experiments","homepage":"/turing","name":"Turing"},{"configuration":{"api":"/feast/api","iconName":"appSearchApp","navigation":[{"destination":"/entities","label":"Entities"},{"destination":"/featuretables","label":"Feature Tables"},{"destination":"/jobs/batch","label":"Batch Ingestion Jobs"},{"destination":"/jobs/stream","label":"Stream Ingestion Jobs"}]},"description":"Platform for managing and serving ML features","homepage":"/feast","name":"Feast"},{"configuration":{"iconName":"pipelineApp"},"description":"Platform for managing ML pipelines","homepage":"/pipeline","name":"Pipelines"}]` | Enabled CaraML applications |
| config.authorization.enabled | bool | `false` |  |
| config.authorization.ketoServerURL | string | `"http://mlp-authorization-keto"` |  |
| config.defaultSecretStorage | object | `{}` | Default Secret Storage for storing secrets. Supported values: "vault". If not specified, secrets will be stored as "internal" secret |
| config.docs | list | `[{"href":"https://github.com/gojek/merlin/blob/main/docs/getting-started/README.md","label":"Merlin User Guide"},{"href":"https://github.com/gojek/turing","label":"Turing User Guide"},{"href":"https://docs.feast.dev/user-guide/overview","label":"Feast User Guide"}]` | Documentation list for caraml components |
| config.environment | string | `"production"` |  |
| config.mlflow.trackingURL | string | `"http://mlflow.mlp"` |  |
| config.oauthClientID | string | `""` | OAuth client id for login |
| config.streams | object | `{}` | Streams list |
| config.ui.clockworkUIHomepage | string | `"http://clockwork.dev"` |  |
| config.ui.kubeflowUIHomepage | string | `"http://kubeflow.org"` |  |
| deployment.extraLabels | object | `{}` | Additional labels to apply on the deployment |
| deployment.image | object | `{"pullPolicy":"IfNotPresent","registry":"ghcr.io","repository":"caraml-dev/mlp","tag":"v1.7.7-build.63-8309142"}` | mlp image related configs |
| deployment.livenessProbe.path | string | `"/v1/internal/live"` |  |
| deployment.podLabels | object | `{}` | Additional labels to apply on the pod level |
| deployment.readinessProbe.path | string | `"/v1/internal/ready"` |  |
| deployment.replicaCount | int | `1` |  |
| deployment.resources | object | `{}` | Configure resource requests and limits, Ref: http://kubernetes.io/docs/user-guide/compute-resources/ |
| deployment.tolerations | list | `[]` |  |
| externalPostgresql.address | string | `"127.0.0.1"` | Host address for the External postgres |
| externalPostgresql.createSecret | bool | `false` |  |
| externalPostgresql.database | string | `"mlp"` | External postgres database schema |
| externalPostgresql.enableProxySidecar | bool | `false` | Enable if you want to configure a sidecar for creating a proxy for your db connections. |
| externalPostgresql.enabled | bool | `false` | If you would like to use an external postgres database, enable it here using this |
| externalPostgresql.password | string | `"password"` |  |
| externalPostgresql.proxyType | string | `"cloudSqlProxy"` | Type of sidecar to be created, mentioned type needs to have the spec below. |
| externalPostgresql.secretKey | string | `"postgresql-password"` | If a secret is created by external systems (eg. Vault)., mention the key under which password is stored in secret (eg. postgresql-password) |
| externalPostgresql.secretName | string | `""` | If a secret is created by external systems (eg. Vault)., mention the secret name here |
| externalPostgresql.sidecarSpec | object | `{"cloudSqlProxy":{"dbConnectionName":"asia-east-1:mlp-db","dbPort":5432,"image":{"tag":"1.33.2"},"resources":{"limits":{"cpu":"1000m","memory":"1G"},"requests":{"cpu":"200m","memory":"512Mi"}},"spec":[{"command":["/cloud_sql_proxy","-ip_address_types=PRIVATE","-log_debug_stdout","-instances={{ .Values.externalPostgresql.sidecarSpec.cloudSqlProxy.dbConnectionName }}=tcp:{{ .Values.externalPostgresql.sidecarSpec.cloudSqlProxy.dbPort }}"],"image":"gcr.io/cloudsql-docker/gce-proxy:{{ .Values.externalPostgresql.sidecarSpec.cloudSqlProxy.image.tag }}","name":"cloud-sql-proxy","resources":{"limits":{"cpu":"1000m","memory":"1G"},"requests":{"cpu":"200m","memory":"512Mi"}},"securityContext":{"runAsNonRoot":true}}]}}` | container spec for the sidecar |
| externalPostgresql.sidecarSpec.cloudSqlProxy | object | `{"dbConnectionName":"asia-east-1:mlp-db","dbPort":5432,"image":{"tag":"1.33.2"},"resources":{"limits":{"cpu":"1000m","memory":"1G"},"requests":{"cpu":"200m","memory":"512Mi"}},"spec":[{"command":["/cloud_sql_proxy","-ip_address_types=PRIVATE","-log_debug_stdout","-instances={{ .Values.externalPostgresql.sidecarSpec.cloudSqlProxy.dbConnectionName }}=tcp:{{ .Values.externalPostgresql.sidecarSpec.cloudSqlProxy.dbPort }}"],"image":"gcr.io/cloudsql-docker/gce-proxy:{{ .Values.externalPostgresql.sidecarSpec.cloudSqlProxy.image.tag }}","name":"cloud-sql-proxy","resources":{"limits":{"cpu":"1000m","memory":"1G"},"requests":{"cpu":"200m","memory":"512Mi"}},"securityContext":{"runAsNonRoot":true}}]}` | container spec for the Google CloudSQL auth proxy sidecar, ref: https://cloud.google.com/sql/docs/postgres/connect-kubernetes-engine |
| externalPostgresql.username | string | `"mlp"` | External postgres database user |
| global.protocol | string | `"http"` |  |
| ingress.enabled | bool | `false` |  |
| postgresql.enabled | bool | `true` | Enable creating mlp specific postgres instance |
| postgresql.nameOverride | string | `"mlp-postgresql"` | override the name here so that db gets created like <release_name>-mlp-postgresql |
| postgresql.persistence.size | string | `"10Gi"` |  |
| postgresql.postgresqlDatabase | string | `"mlp"` |  |
| postgresql.postgresqlUsername | string | `"mlp"` |  |
| postgresql.resources | object | `{}` | Configure resource requests and limits, Ref: http://kubernetes.io/docs/user-guide/compute-resources/ |
| sentry.dsn | string | `""` | Sentry DSN value used by both Turing API and Turing UI |
| service.externalPort | int | `8080` |  |
| service.internalPort | int | `8080` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `"mlp"` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.11.0](https://github.com/norwoodj/helm-docs/releases/v1.11.0)
