# 🟢 Deployments

### Overview

In the deployment overview, you can see the counts of: **rollouts**, **instances**, **interfaces**, **volumes**, **envs** and **secrets**. You can also see the current container image. There is also a cpu and memory usage graph for the project. (keep in mind this is a **live** usage view, for tracking usage please use something like the [https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack))

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>apache deployment overview</p></figcaption></figure>

### Deployment settings

In the project settings, you can change the project **name**, **description**, and **labels**. You can also **delete** the project from the project settings. There is also an option to use _advanced editing_ mode for the project. Head over to the [crd.md](../operator-manual/crd.md "mention") section to learn more about the Operator CRD. You can also directly create a new **blueprint** from the selected project.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

#### Advanced editing

{% hint style="info" %}
There is **no validation** on what you configure in advanced editing. Make sure you know the configuration accoring to the Operator CRD. If something breaks, you can easily **rollback** in the [rollouts.md](rollouts.md "mention").
{% endhint %}

With advanced editing, you can add settings to the project that are not available in the UI. You can also see the raw CRD of the deployment.

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption><p>advanced editing</p></figcaption></figure>

#### New blueprint from deployment

With a new blueprint from the deployment, you can create a new blueprint with the same settings as the selected deployment. The only thing which is **not** copied are the **ingress** **settings**.

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption><p>new blueprint from deployment</p></figcaption></figure>
