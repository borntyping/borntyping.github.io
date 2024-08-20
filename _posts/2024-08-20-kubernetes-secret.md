---
title: Can you use a Kubernetes secret from another namespace? 
short: Cross-namespace k8s secrets
category: Development
tags: TIL
layout: post
date: "2024-08-20"
---

Yes, and no:

- A Pod can only reference a Secret in the same namespace[^1].
- RBAC can allow a ServiceAccount access to Secrets in other namespaces[^2].

[^1]: See [imagePullReference](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#containers) and [envFrom](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#environment-variables) in the Pod API spec.
[^2]: Which is how operators that manage secrets across multiple namespaces work.
