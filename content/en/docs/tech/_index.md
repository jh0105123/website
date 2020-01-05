---
title: Tech.
main_menu: true
content_template: templates/concept
weight: 80
---

{{% capture overview %}}

The Concepts section helps you learn about the parts of the Kubernetes system and the abstractions Kubernetes uses to represent your {{< glossary_tooltip text="cluster" term_id="cluster" length="all" >}}, and helps you obtain a deeper understanding of how Kubernetes works.

{{% /capture %}}

{{% capture body %}}

## Overview
hello
- **`monospace bold`**
- {{<color value="red" text="중요">}}

```
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
```
{{% /capture %}}
{{< image src="/images/kubernetes-horizontal-color.png" width="400" >}}
