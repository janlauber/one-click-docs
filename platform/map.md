# 🗺️ Map

The map feature in a deployment uses [svelte-flow](https://svelteflow.dev/) to graphically show the resources of the current rollout in the selected deployment. Everything gets updated in real time via a websocket endpoint described in the pocketbase docs: [pocketbase.md](pocketbase.md "mention")

You can move the components with your mouse, zoom in and out and dig into its configurations / logs / events when click on a component.

<figure><img src="../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

### Component Details

When clicking on a component you can see its current applied manifest in-cluster configurations. This will give you some more information about the component itself.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>manifest</p></figcaption></figure>

When selecting a pod you can also see it's logs directly streamed:

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>pod logs</p></figcaption></figure>

Also for the pod you can see the events which happen inside the cluster. This will also help you to troubleshoot your rollouts.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>events</p></figcaption></figure>

### Deleting a pod

You also have the ability to delete a selected pod by clicking on the <mark style="color:red;">red trash</mark> icon.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>deleting a pod</p></figcaption></figure>
