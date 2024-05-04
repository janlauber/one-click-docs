# 💾 Image

Under images you can manage the image of the deployment. You can configure the **registry** (e.g. ghcr.io, docker.io), your **username** and **password** if it's private and also the **repository**/**image**. Last but not least you can define the image **tag**. If you need to debug something you can copy the current rollout ID to search the components inside the Kubernetes cluster.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p>configuration</p></figcaption></figure>

### Auto update

If you don't want to manually update your image tag each time you push a new version of your image to the registry you can activate the **Auto Update** feature. There you can specify an interval (1m, 5m, 10m), a pattern and policy how the image registry should get checked and the image should get updated.

* Interval: the cron ticker defined in the [pocketbase.md](pocketbase.md "mention") environment variable will check the modulo of the minutes and checks the registry in this interval. So it's crucial to let the cron tick interval at 1m as it is default.
* Pattern: a regex pattern which parses the image tag. The default is the default semver notation x.x.x
* Policy: the policy (**semver** or **timestamp**) defines the sorting. For timestamp it will only work if the image tag is a **unix** timestamp.

The behaviour and consept is similar to the one of fluxcd: [**https://fluxcd.io/flux/guides/image-update/**](https://fluxcd.io/flux/guides/image-update/)

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>auto update</p></figcaption></figure>

#### Examples

<table><thead><tr><th>Pattern</th><th width="249">Policy</th><th>Note</th></tr></thead><tbody><tr><td>^\d+.\d+.\d+$</td><td>semver</td><td>Default x.x.x semver pattern. e.g. 1.2.0 will get updated to 1.2.1</td></tr><tr><td>dev-\d+.\d+.\d+$</td><td>semver</td><td>Default x.x.x semver pattern with a <strong>dev-</strong> prefix.</td></tr><tr><td>.*</td><td>timestamp</td><td>Any pattern will get updated with a <strong>unix</strong> timestamp.</td></tr><tr><td>preview-*</td><td>timestamp</td><td>A pattern with the <strong>preview-</strong> prefix which will get udpated with a <strong>unix</strong> timestamp.</td></tr></tbody></table>
