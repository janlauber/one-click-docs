# 🔐 Envs & Secrets

On the envs & secrets page you can configure the environment variables and secrets for your application. The environment variables are key-value pairs that are injected into the container. The secrets are sensitive data that are stored as **Kubernetes secrets**. The secrets are base64 encoded and can be used as environment variables or mounted as files. You can simply copy and paste the content of your `.env` file or secret file into the text area.

Both the environment variables and secrets are available in the container as **environment** variables.

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption><p>envs &#x26; secrets overview</p></figcaption></figure>
