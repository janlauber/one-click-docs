# Platform Installation

One-Click can run inside or outside of a Kubernetes cluster.

You will need the following to run OneClick:

* [Kubernetes](https://kubernetes.io/) cluster
* [Docker](https://www.docker.com/) daemon
* [Node.js](https://nodejs.org/en/) v18.16.0 or higher
* [npm](https://www.npmjs.com/) v9.5.1 or higher
* [Go](https://golang.org/)
* [Kubectl](https://kubernetes.io/docs/tasks/tools/)
* [Kustomize](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/)

### Installation

{% hint style="info" %}
You can also run the one-click container outside of the corresponding Kubernetes cluster and make sure it has access to the `~/.kube/config` of the executing user and the env `LOCAL=true` set.
{% endhint %}

1. Install the Operator Follow the installation instructions provided in the [one-click-operator repository](https://github.com/janlauber/one-click-operator) or in the [setup-guide.md](../operator-manual/setup-guide.md "mention")
2.  Install the UI & Backend Check out the [deployment](https://github.com/janlauber/one-click/tree/main/deployment) folder and change the values for your environment. Then run the following commands:

    ```sh
    cd deployment
    kubectl apply -k .
    ```
3.  Access the UI

    ```sh
    # if you are using an ingress
    kubectl get ingress -n one-click
    # if you want to use port-forwarding
    kubectl port-forward -n one-click svc/one-click-ui 8080:80
    ```
4. Access Pocketbase on your URL or localhost:8080 with `/_` as the path. Example: `localhost:8080/_`. You should see the Pocketbase UI and set your admin user. Then create a new user under `users` collection. You can now login with your new user.

Head over to the [pocketbase.md](../platform/pocketbase.md "mention")docs to get more information why we use pocketbase and how you can adminstrate it.

### Helm

{% hint style="info" %}
The helm chart is not yet done. I've you got some time you can help us out!
{% endhint %}

```bash
helm repo add one-click https://charts.one-click.dev
helm upgrade --install one-click/one-click
```
