# ↔️ Scale

On the scale page you can configure the two scaling options **horizontal** and **vertical**. The horizontal scaling is the number of instances (replicas) and the vertical scaling is the CPU and memory request and limit.

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption><p>scale</p></figcaption></figure>

### Horizontal

You can define the number of minimum and maximum replicas. The **target CPU** defines the autoscaling behaviour. If the CPU usage is above the target CPU the replicas will get scaled up. To get the current CPU usage you can head over to the project **overview** page.

### Vertical

The vertical scaling is the CPU and memory request and limit. The request is the minimum amount of CPU and memory the pod will get. The limit is the maximum amount of CPU and memory the pod will get. If the pod exceeds the limit it will get terminated. The request and limit are defined in **millicores** and **mega bytes**. The limit should be equal or higher than the request.

Make sure to know your application requirements to set the right values. If you don't know the requirements you can start with the default values and monitor the behaviour. If you see that the pod gets terminated because of the limit you can increase the limit.
