# 🧬 CRD

The development of the Kubernetes operator, housed in the "[one-click-operator](https://github.com/janlauber/one-click-operator)" repository, involves multiple key components and processes. Central to this is the `rollout_types.go` file, where the structures for the Rollout Custom Resource Definition (CRD) are defined. These structures are crucial because they dictate the configuration and capabilities of the Rollout CRD. The operator-sdk, known for its user-friendliness, is then used to generate corresponding YAML files. These files are stored in the "config" folder, signifying their role in configuring the operator.

The operator is designed with a specific domain, "**one-click.dev**", and uses the API CRD version "**v1alpha1**". This versioning indicates that the operator is in its early stages of development and is not yet considered production-ready—a common practice in the Kubernetes community. For guidance on best practices in developing Kubernetes operators using the operator-sdk, resources are available at [https://sdk.operatorframework.io/docs/best-practices/best-practices/](https://sdk.operatorframework.io/docs/best-practices/best-practices/).

Following the CRD definition, the next step involves the implementation of the operator's logic. This is where the concept of abstraction becomes pivotal. The operator aims to simplify the management and creation of various Kubernetes objects by consolidating them into a single CRD— the Rollout CRD. This abstraction is particularly beneficial for the backend of the One-Click platform, as it reduces the complexity of managing multiple Kubernetes resources. Instead, the platform can focus on managing just the Rollout CRD.

The Kubernetes objects included in this abstraction are:

* Deployment
  * Environment Variables
  * Volumes
  * Image Pull Secret
* Horizontal Pod Autoscaler
* Secret
* Persistent Volume Claims
* Services
* Ingresses
* Service Account

Each of these components plays a vital role in the Kubernetes ecosystem, contributing to aspects like deployment management, security, scaling, and connectivity.

In the "controllers" folder, you'll find the `rollout_controller.go` file, which is integral to the operator's functionality. This file contains the `Reconcile()` function, a critical component that interacts with the Kubernetes API. The Reconcile function acts as the heart of the operator, responding to changes and ensuring that the desired state of the Kubernetes objects is maintained. For each Kubernetes object listed above, separate Go files are created. These files encapsulate the specific logic required to manage each object, thereby modularizing the code and making it more manageable and maintainable.

To further elaborate on the Kubernetes operator development, let's delve deeper into the `Reconcile()` function and the concept of the owner functionality.

{% code title="rollout.yaml" lineNumbers="true" fullWidth="true" %}
```yaml
apiVersion: one-click.dev/v1alpha1
kind: Rollout
metadata:
  name: nginx
  namespace: test
spec:
  args: ["nginx", "-g", "daemon off;"]
  command: ["nginx"]
  rolloutStrategy: rollingUpdate # or "recreate" (if not specified then "rollingUpdate" is used)
  nodeSelector:
    kubernetes.io/hostname: minikube
  tolerations:
    - key: "storage"
      operator: "Equal"
      value: "ssd"
      effect: "NoSchedule"
  image:
    registry: "docker.io"
    repository: "nginx"
    tag: "latest"
    username: "test"
    password: "test3"
  securityContext: # can also be set to {}
    runAsUser: 1000
    runAsGroup: 1000
    fsGroup: 1000
    allowPrivilegeEscalation: false
    runAsNonRoot: true
    readOnlyRootFilesystem: true
    privileged: false
    capabilities:
      drop:
        - ALL
      add:
        - NET_BIND_SERVICE
  horizontalScale:
    minReplicas: 1
    maxReplicas: 3
    targetCPUUtilizationPercentage: 80
  resources:
    requests:
      cpu: "100m"
      memory: "128Mi"
    limits:
      cpu: "200m"
      memory: "256Mi"
  env:
    - name: "REFLEX_USERNAME"
      value: "admin"
    - name: DEBUG
      value: "true"
  secrets:
    - name: "REFLEX_PASSWORD"
      value: "admin"
    - name: "ANOTHER_SECRET"
      value: "122"
  volumes:
    - name: "data"
      mountPath: "/data"
      size: "2Gi"
      storageClass: "standard"
  interfaces:
    - name: "http"
      port: 80
    - name: "https"
      port: 443
      ingress:
        ingressClass: "nginx"
        annotations:
          nginx.ingress.kubernetes.io/rewrite-target: /
          nginx.ingress.kubernetes.io/ssl-redirect: "false"
        rules:
          - host: "reflex.oneclickapps.dev"
            path: "/"
            tls: true
            tlsSecretName: "wildcard-tls-secret"
          - host: "reflex.oneclickapps.dev"
            path: "/test"
            tls: false
  cronjobs:
    - name: some-bash-job
      suspend: false
      image:
        password: ""
        registry: docker.io
        repository: library/busybox
        tag: latest
        username: ""
      schedule: "*/1 * * * *"
      command: ["echo", "hello"]
      maxRetries: 3
      backoffLimit: 2
      env:
        - name: SOME_ENV
          value: "some-value"
      resources:
        limits:
          cpu: 500m
          memory: 512Mi
        requests:
          cpu: 100m
          memory: 256Mi
  serviceAccountName: "nginx"
```
{% endcode %}
