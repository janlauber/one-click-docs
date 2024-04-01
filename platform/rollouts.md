# ⏱️ Rollouts

Each time you edit and change something in a project a new rollout will get created. This is like a **snapshot** of your [crd.md](../operator-manual/crd.md "mention") configuration. This gives you the power to undo any changes you did to your project configuration like changing the port of an interface or updating your image tag. You can see every rollout in the rollouts table. Through the frontend you won't be able to delete a rollout, you can just hide it. This is due to get some statistics about you rollouts. If you need to delete a rollout completely you need to go to the pocketbase backend and delete the record in the "rollouts" collection.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>rollouts overview</p></figcaption></figure>

### Rollback diff

When selecting a previous rollout you can click on "rollback" and then a diff shows up which diffs the CRD files and show you exactly what will change:

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>rollout diff</p></figcaption></figure>

### Hidden rollouts

When you have hidden rollouts you can show them by toggle the "Show hidden" slider:

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>hidden rollouts</p></figcaption></figure>

### Insights

You can also see some more insights (like events) of the running rollout by expanding the sidebar:

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>rollout insights</p></figcaption></figure>

