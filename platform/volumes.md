# 💿 Volumes

For persistent storage, you can define volumes. The volumes are the persistent storage for your application. You can define as many volumes as you want. To create a new volume you can click the **New Volume** button.

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption><p>new volume</p></figcaption></figure>

You can define the following options:

* name: the name of the volume, must be unique in the **deployment**
* mount path: the mount path of the volume (e.g. /data, /var/lib/mysql)
* size: the size of the volume in **GiB** (gibibyte)
* storage class: the storage class of the volume (the dropdown will show you the available storage classes inside the Kubernetes cluster)

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption><p>volume overview</p></figcaption></figure>

{% hint style="info" %}
You cannot change the size or storage class of a volume after creation. If you need to change the size or storage class you need to create a new volume and migrate the data.
{% endhint %}
