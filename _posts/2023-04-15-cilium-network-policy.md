---
layout: page
title: "Block egress traffic with Cilium network plugin"
categories: Go
---

# Introduction
In a previous post  [How I tried to create resilience test for NATS in Kubernetes?]({% post_url 2023-04-09-resilience-testing-k8s %}) I described a problem of testing software during unexpected loosing of connection or deny of external service, but in that post I told that there is no way to interrupt TCP connection by Kubernetes Network Policy. I was wrong, there is a way to do so. I just used another k8s network plugin where interruption of live TCP connection didn't worked. But I found a solution and name for it - Cilium Network Policy

# Cilium Network Policy
Cilium - is just another network policy for Kubernetes which should be installed first to be used which gives a possibility to achieve my target: block traffic to one pod and terminate exists TCP connections.

I created PoC project for test Cilium Network Policy which can be accessed at [GitHub](https://github.com/vitalii-honchar/cilium-network-policy-poc).

Network policy which blocks all traffic from a pod looks like:
```YAML
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
  name: deny-server-egress
  namespace: server
spec:
  endpointSelector:
    matchLabels:
      app: server
      name: server
  egress: 
  - {}
```

The same like a network policy from my previous post, but just changed `apiVersion` and `kind`.

# Pods logs after blocked traffic

![Screenshot](/attachments/2023-04-15-cilium-network-policy/screenshot.png)

# Conclusions
As conclusion I want to say that during solving software problem I should try more to use already exists solutions rather than implement my own which I like too much.
Modern search technologies, like ChatGPT or Google gives me a possibility to find another ways to achieve my target with sophisticated solution without recreated system architecture again.

# Resources
1. [Cilium docs](https://docs.cilium.io/en/stable/overview/intro/)
2. [Kubernetes Network Policies with Cilium](https://medium.com/rahasak/kubernetes-network-policies-with-cilium-17be223fe67b)