# 👖 Pocketbase

One-Click uses the open source backend [pocketbase](https://pocketbase.io) to achieve things like authentication and storing data. It also serves the frontend of One-Click. In the release process the pocketbase and frontend code will get compiled and put into a single container image and pushed to the Github container registry.

Pocketbase offers the ability to extend it with our own golang code. You can listen on certain events and then execute code. We use that to make the Kubernetes api calls and manage the Kubernetes resources created via the frontend interface.

You can find the code under the following link: [https://github.com/janlauber/one-click/tree/main/pocketbase](https://github.com/janlauber/one-click/tree/main/pocketbase)

## Authentication

Pocketbase uses JWT tokens for authentication. The frontend sends a request to the pocketbase backend with the user credentials. The backend then checks if the user exists and if the password is correct. If everything is correct, the backend will return a JWT token. The frontend will then store this token in the local storage and use it for every request to the backend.

We also support the ability to use the following authentication providers:

- Google
- Github
- Microsoft

The frontend will automatically display the login buttons for these providers if they are enabled in the pocketbase backend.

## Custom Endpoints



## Environment Variables

| Variable Name | Default       | Description                                                                                                                        |
| ------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `LOCAL`       | `false`       | Set to `true` if you're running KubeLab locally. It will take your local kubeconfig under **.kube/config**                         |
| `CronTick`    | `*/1 * * * *` | The tick in cron notation at which the auto image update will check for new updates in the registry. Do not change this under 1min |
