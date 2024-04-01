# 🏗️ Architecture

The following diagram shows how and what the One-Click operator manages.

In <mark style="color:red;">red</mark> you see everything responsible for the frontend / pocketbase backend.\
In <mark style="color:blue;">blue</mark> you see everything which handles Kubernetes natively.\
In <mark style="color:green;">green</mark> you see what the One-Click operator manages and controls.

Every Kubernetes resource will get created and managed within a Kubernetes namespace named with the `project ID`

<img src="../.gitbook/assets/file.excalidraw.svg" alt="architecture" class="gitbook-drawing">

The architecture of the solution is designed to operate within a Kubernetes ecosystem, focusing on simplicity and manageability for deploying containers. Here is a high-level view of its main components:

* **Frontend Component**: Developed with Svelte, the frontend provides the user interface. Its primary role is to facilitate user interaction and input, which it relays to the backend for processing.
* **Backend System**: The backend, powered by Pocketbase, acts as the central processing unit. It interprets requests from the frontend, managing the necessary API calls and interactions within the Kubernetes environment.
* **Kubernetes Cluster Interaction**: The backend is responsible for orchestrating various elements within the Kubernetes cluster. A key function includes the creation and management of namespaces, segregating projects to maintain orderly and isolated operational environments.
* **Custom Resource Management (Rollouts)**: Rollouts, defined as Custom Resource Definitions (CRDs) within Kubernetes, are managed by the backend. These are central to the deployment and operational processes, serving as bespoke objects tailored to the system's requirements.
* **One-Click Kubernetes Operato**r: This component simplifies interactions with Kubernetes. It automates the handling of several Kubernetes native objects and processes, including deployments, scaling, and resource allocation. The operator is crucial for streamlining complex tasks and ensuring efficient system operations.
* **System Scalability**: The architecture is designed with scalability in mind, using Kubernetes' capabilities to handle a range of workloads and adapting as necessary for different project sizes and requirements.

This architecture aims to streamline the deployment process for OSS containers, offering an efficient and manageable system that leverages the strengths of [Kubernetes](https://kubernetes.io), [Svelte](https://svelte.dev), and [Pocketbase](https://pocketbase.io).
