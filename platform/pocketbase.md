# 👖 Pocketbase

One-Click uses the open source backend [pocketbase](https://pocketbase.io) to achieve things like authentication and storing data. It also serves the frontend of One-Click. In the release process the pocketbase and frontend code will get compiled and put into a single container image and pushed to the Github container registry.

Pocketbase offers the ability to extend it with our own golang code. You can listen on certain events and then execute code. We use that to make the Kubernetes api calls and manage the Kubernetes resources created via the frontend interface.

You can find the code under the following link: [https://github.com/janlauber/one-click/tree/main/pocketbase](https://github.com/janlauber/one-click/tree/main/pocketbase)

## Authentication



## Custom Endpoints



## Environment Variables

| Variable Name | Default       | Description                                                                                                                        |
| ------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `LOCAL`       | `false`       | Set to `true` if you're running KubeLab locally. It will take your local kubeconfig under **.kube/config**                         |
| `CronTick`    | `*/1 * * * *` | The tick in cron notation at which the auto image update will check for new updates in the registry. Do not change this under 1min |
