# 🏗️ Architecture

The following diagram shows how and what the One-Click operator manages.

In <mark style="color:red;">red</mark> you see everything responsible for the frontend / pocketbase backend. \
In <mark style="color:blue;">blue</mark> you see everything which handles Kubernetes natively.\
In <mark style="color:green;">green</mark> you see what the One-Click operator manages and controls.

Every Kubernetes resource will get created and managed within a Kubernetes namespace named with the `project ID`

<img src="../.gitbook/assets/file.excalidraw.svg" alt="architecture" class="gitbook-drawing">
