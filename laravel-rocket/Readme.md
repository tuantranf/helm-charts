# laravel-rocket-helm-chart

## Usage

### Setup Helm Tiller

### Add Helm repository

```bash
helm repo add laravel-rocket-helm-chart https://tuantranf.github.io/laravel-rocket-helm-chart
helm repo update
```

### Configure values file

```yaml
# Default values for laravel-rocket.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

replicaCount: 1

app:
  # please update your docker image
  repository: chart-example
  tag: latest
  pullPolicy: Always
  envFilePath: "app.env"

service:
  type: ClusterIP
  port: 80

ingress:
  enabled: false
  annotations: {}
    # kubernetes.io/ingress.class: nginx
    # kubernetes.io/tls-acme: "true"
  path: /
  hosts:
    - chart-example.local
  tls: []
  #  - secretName: chart-example-tls
  #    hosts:
  #      - chart-example.local

resources: {}
  # We usually recommend not to specify default resources and to leave this as a conscious
  # choice for the user. This also increases chances charts run on environments with little
  # resources, such as Minikube. If you do want to specify resources, uncomment the following
  # lines, adjust them as necessary, and remove the curly braces after 'resources:'.
  # limits:
  #  cpu: 100m
  #  memory: 128Mi
  # requests:
  #  cpu: 100m
  #  memory: 128Mi

nodeSelector: {}

tolerations: []

affinity: {}

```

### Install application

```bash
helm upgrade --install --force chart-example -f ./values.yml laravel-rocket-helm-chart/laravel-rocket --wait
```
