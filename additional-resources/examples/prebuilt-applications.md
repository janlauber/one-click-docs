# Prebuilt Applications

## Node-Red

{% embed url="https://nodered.org/" %}

Node-RED is a programming tool for wiring together hardware devices, APIs and online services in new and interesting ways.

```yaml
apiVersion: one-click.dev/v1alpha1
kind: Rollout
spec:
  env: []
  horizontalScale:
    maxReplicas: 1
    minReplicas: 1
    targetCPUUtilizationPercentage: 80
  image:
    password: ''
    registry: docker.io
    repository: nodered/node-red
    tag: latest
    username: ''
  interfaces:
    - name: http
      port: 1880
  resources:
    limits:
      cpu: 500m
      memory: 512Mi
    requests:
      cpu: 300m
      memory: 256Mi
  secrets: []
  serviceAccountName: one-click
  volumes:
    - mountPath: /data
      name: data
      size: 1Gi
      storageClass: '' # replace with your storage class
```

## Pocketbase

{% embed url="https://pocketbase.io/" %}

Pocketbase is an open-source, self-hosted firebase alternative.

```yaml
apiVersion: one-click.dev/v1alpha1
kind: Rollout
spec:
  env: []
  horizontalScale:
    maxReplicas: 1
    minReplicas: 1
    targetCPUUtilizationPercentage: 80
  image:
    password: ''
    registry: ghcr.io
    repository: muchobien/pocketbase
    tag: latest
    username: ''
  interfaces:
    - name: http
      port: 8090
  resources:
    limits:
      cpu: 500m
      memory: 512Mi
    requests:
      cpu: 300m
      memory: 256Mi
  secrets: []
  serviceAccountName: one-click
  volumes:
    - mountPath: /pb_data
      name: pb-data
      size: 1Gi
      storageClass: '' # replace with your storage class
```

## Ghost

{% embed url="https://ghost.org/" %}

Ghost is a professional publishing platform. 
In production, you should use a mysql database.
This is an example of a multi-deployment setup with MySQL and Ghost.

### MySQL

```yaml
apiVersion: one-click.dev/v1alpha1
kind: Rollout
spec:
  env:
    - name: MYSQL_DATABASE
      value: ghost
    - name: MYSQL_USER
      value: admin
  horizontalScale:
    maxReplicas: 1
    minReplicas: 1
    targetCPUUtilizationPercentage: 80
  image:
    password: ''
    registry: docker.io
    repository: library/mysql
    tag: latest
    username: ''
  interfaces:
    - name: mysql
      port: 3306
  resources:
    limits:
      cpu: 500m
      memory: 1024Mi
    requests:
      cpu: 300m
      memory: 512Mi
  secrets:
    - name: MYSQL_ROOT_PASSWORD
      value: password
    - name: MYSQL_PASSWORD
      value: password
  serviceAccountName: one-click
  volumes:
    - mountPath: /var/lib/mysql
      name: data
      size: 1Gi
      storageClass: '' # replace with your storage class
```

### Ghost

```yaml
apiVersion: one-click.dev/v1alpha1
kind: Rollout
spec:
  env:
    - name: database__client
      value: mysql
    - name: database__connection__host
      value: mysql-12pr47a4cgcr9rx-svc # replace with your mysql service name (printed in the interface section of the mysql deployment)
    - name: database__connection__user
      value: admin
    - name: database__connection__database
      value: ghost
    - name: url
      value: https://ghost.one-click.dev
  horizontalScale:
    maxReplicas: 1
    minReplicas: 1
    targetCPUUtilizationPercentage: 80
  image:
    password: ''
    registry: docker.io
    repository: library/ghost
    tag: latest
    username: ''
  interfaces:
    - ingress:
        ingressClass: nginx-external # replace with your ingress class
        rules:
          - host: ghost.one-click.dev
            path: /
            tls: true
            tlsSecretName: wildcard-cert # replace with your tls secret name
      name: http
      port: 2368
  resources:
    limits:
      cpu: 500m
      memory: 512Mi
    requests:
      cpu: 300m
      memory: 256Mi
  secrets:
    - name: database__connection__password
      value: password
  serviceAccountName: one-click
  volumes:
    - mountPath: /var/lib/ghost/content
      name: data
      size: 1Gi
      storageClass: '' # replace with your storage class
```
