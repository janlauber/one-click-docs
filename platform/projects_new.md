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

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>project card</p></figcaption></figure>

### Overview

In the project overview, you can see the counts of: rollouts, instances, interfaces, volumes, envs and secrets. You can also see the current container image. There is also a cpu and memory usage graph for the project.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>project overview</p></figcaption></figure>

### Project settings

In the project settings, you can change the project **name**, **description**, and **labels**. You can also **delete** the project from the project settings. There is also an option to use _advanced editing_ mode for the project. Head over to the [crd.md](../operator-manual/crd.md "mention") section to learn more about the Operator CRD. You can also directly create a new **blueprint** from the selected project.

#### Project settings

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>project settings</p></figcaption></figure>

#### Advanced editing

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>advanced editing</p></figcaption></figure>

#### New blueprint from project

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>new blueprint from project</p></figcaption></figure>
