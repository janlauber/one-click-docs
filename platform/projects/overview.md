# Overview

In One-Click you can create a new project or manage existing ones. Each project will get a unique `ID` which will be used to identify the project inside the Kubernetes cluster. The project will also get a unique `namespace` in the Kubernetes cluster which has the same name as the project `ID`.

## Create a new project

To create a new project, log in to the One-Click platform and click on the top right corner `New Project` button. Fill in the project name and description and select a `blueprint` to use for the project. Click on the `Create project` button to create the project.

{% hint style="info" %}
You first need to create a blueprint before you can create a project. Head over to the [blueprints.md](../blueprints.md "mention") section to learn more about blueprints.
{% endhint %}

You can also set some labels for the project. Labels are used to group projects together and can be used to filter projects in the project list.

## Manage existing projects

Each project has it's own overview page where you can see the details of the project and it's resources.

### Project settings

In the project settings, you can change the project name, description, and labels. You can also delete the project from the project settings.
There is also an option to use advanced editing mode for the project. Head over to the [Operator CRD](../../operator-manual/crd.md "mention") section to learn more about the Operator CRD.
You can also directly create a new blueprint from the selected project.
