# 📂 Projects

In One-Click you can create a new project or manage existing ones. Each project will get a unique `ID` which will be used to identify the project inside the Kubernetes cluster. The project will also get a unique `namespace` in the Kubernetes cluster which has the same name as the project `ID`.

## Create a new project

To create a new project, log in to the One-Click platform and click on the top right corner `New Project` button. Fill in the project name and description and select a `blueprint` to use for the project. Click on the `Create project` button to create the project.

{% hint style="info" %}
You first need to create a blueprint before you can create a project. Head over to the [blueprints.md](blueprints.md "mention") section to learn more about blueprints.
{% endhint %}

You can also set some labels for the project. Labels are used to group projects together and can be used to filter projects in the project list.

## Manage existing projects

Each project has it's own overview page where you can see the details of the project and it's resources.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>sample project</p></figcaption></figure>

There will be a Kubernetes namespace each One-Click project with certain labels:

| label                     | description                           |
| ------------------------- | ------------------------------------- |
| one-click.dev/displayName | The users display name in pocketbase. |
| one-click.dev/projectId   | The project name which is the ID.     |
| one-click.dev/userId      | The users ID of the project.          |
| one-click.dev/username    | The username of the project.          |

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>In cluster namespace labels</p></figcaption></figure>

### Overview

In the project overview, you can see all the deployments in this project. You can also navigate to the **Blueprints**, create a **new Deployment** or make some **project settings**. In the listed deployments you can see it's status, the **ID** of the current rollout, the **amount** of running **replicas** in the cluster and the current **image** deployed.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Project overview</p></figcaption></figure>

### Project settings

In the project settings, you can change the project **name**, **avatar** and **labels**. You can also delete the project from the project settings which will also delete the **namespace** in the Kubernetes cluster.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
