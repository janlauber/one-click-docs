# 🔀 Network

For the network, you have a few options to configure. You can define as many services and ingress interfaces as you want. The services are the internal Kubernetes services and the ingress is the external access to your services. To create a new network interface you can click the **New Interface** button.

<figure><img src="../.gitbook/assets/image (14) (1).png" alt=""><figcaption><p>new interface</p></figcaption></figure>

You can define the following options:

* name: the name of the interface, must be unique in the **deployment**
* port: the port of the interface (take your application port, defined in the Dockerfile)
* ingress class: the ingress class of the interface (the dropdown will show you the available ingress classes inside the Kubernetes cluster)
* host: the host of the interface (e.g. example.com)
* path: the path of the interface (e.g. /api, /)
* tls: if you want to use TLS you can toggle the switch and define the secret name
* (tls secret name: the secret name of the TLS certificate) if not defined it will default to the host name -> use case: you want to auto-generate the TLS certificate with cert-manager annotation

The <mark style="color:green;">**DNS name**</mark> is the actual Kubernetes Service name in the cluster. This name you can use in other deployments to connect to the service via DNS lookup. (click on the copy icon to copy the name).

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption><p>interfaces overview</p></figcaption></figure>

{% hint style="info" %}
If you set the ingress class to **none**, **remove** the host and path and disable the TLS switch, the ingress will get deleted and only the service will get created. This is useful if you want to expose the service only internally for other services **inside** the Kubernetes cluster.
{% endhint %}
