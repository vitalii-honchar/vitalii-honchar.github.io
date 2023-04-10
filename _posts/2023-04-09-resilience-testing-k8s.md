---
layout: page
title: "How I tried to create resilience test for NATS in Kubernetes?"
categories: Go
---
# Introduction
I'm exploring Kubernetes possibilities and I think about a very interesting problem.

How can I provide resilience test for Go application with NATS message broker?

## Initial resilience test architecture

![Initial resilience test architecture](/attachments/2023-04-09-resilience-k8s/test-overview.png)

Idea of an architecture:
1. Service handles business flows
2. Test deactivates NATS
3. Service continue handle business flows, but fails to publish events to NATS
4. After some time test activates NATS and checks that service restored system state successfully

Restrictions of this architecture: 
* I can't just shutdown NATS, because there are another services which uses this NATS and my test can't interrupt work for another tests.
* This should be test for a service in Kubernetes deployment.
* I can't use Toxiproxy or another proxies, because them can have an impact on application performance for another tests and deploy another infrastructure only for this tests is overcomplicated solution.

# My first thoughts 

To solve described problem above first of all I think to use [Kubernetes Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/), because I can just block egress traffic from my service to NATS pods, in this way simulate service outage. Network policy for block egress traffic looks like:
```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-egress-to-nats
  namespace: app
spec:
  podSelector:
    matchLabels:
      name: app
  policyTypes:
    - Egress
  egress: []
```

Everything looks good and I started testing, but there was a problem: network policy can block all new connections and there is no possibility for terminate already exists connections with network policy. As far as NATS client uses TCP connection, so I can't dynamically create this policy and restrict traffic to NATS. I can create this policy, then deploy my application, only after that policy will works or restart pods of my service, but this is not my case, because I don't want to deploy my pods or restart them every time when I want to run my test. 

**Network policy which blocks egress traffic can't terminate exists TCP connections.**

This was bad, because it means that I can't use network policy for solve my problem.

# Solution

There is another way to achieve simulation of NATS outage: use feature toggles in the service for enable or disable NATS connection.
As far as I don't want to have test endpoints in my application at production environment, I want to have possibility enable or disable this endpoints. [Feature toggles](https://martinfowler.com/articles/feature-toggles.html) are an ideal solution for this.

![Solution](/attachments/2023-04-09-resilience-k8s/disable-nats.png)

I used NATS to delivery a message about disable/enable NATS connection to service, because there is a possibility that not one node will be deployed and if service will subscribe on a management subject without group, so each node in cluster will receive a message and close a NATS connection.

Feature toggles will protect service deployment in production from deploy management code, so even if I will have in code non production code, my production will be protected.

# Conclusions
I expected to use Kubernetes Network Policy to implement this kind of resilience tests and I spent more time on weekends to figure out how to prepare Network Policy, but I recognized that Network Policy is not a solution for this problem. Anyway it was very interesting to investigate Network Policy usage. Btw, not only NATS client has TCP connection, by default Go HTTP client has connection keep alive feature enabled, thus network policies will not cover resilience tests for couple of services which communicates throughout HTTP without pod restart too (or at least need to wait some time for terminate connection).

As far as I spent more time on an investigate than I expected, I didn't provided working code for this post, only diagrams.

# Resources
* [Quickstart for Calico on minikube](https://docs.tigera.io/calico/latest/getting-started/kubernetes/minikube)
* [Kubernetes Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
* [Kubernetes Certified Application Developer (CKAD) with Tests](https://www.udemy.com/course/certified-kubernetes-application-developer/)
* [Minikube](https://minikube.sigs.k8s.io/docs/handbook/pushing/)
* [Deny Egress Traffic](https://github.com/ahmetb/kubernetes-network-policy-recipes/blob/master/11-deny-egress-traffic-from-an-application.md)
* [Feature toggles](https://martinfowler.com/articles/feature-toggles.html)