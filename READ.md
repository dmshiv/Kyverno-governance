# Enforced Automated K8s Cluster Security Using Kyverno Policy Generator and Argo CD

## 🚨 Problem

Kubernetes clusters can become unstable when Pods lack CPU & memory requests/limits. Manual checks don’t scale, and enforcing standards is tough.

## 🛡️ Solution

- Automated policy enforcement with Kyverno: every Pod must declare resource requests/limits.
- GitOps workflow: policies are managed in GitHub and synced to the cluster using Argo CD.
- Switching between audit and enforce modes is seamless—just update a Git branch, and Argo CD applies the change.

## 📦 Files

- `kyverno-policy-allow-pod-creation-if-it-has-resource-limits-else-no.yaml`: Kyverno ClusterPolicy enforcing resource requests/limits.
- `pod-with-no-resource-limit.yaml`: Example Pod (should be blocked by policy).
- `pod-with-resource-limit.yaml`: Example Pod (should be allowed).
- `Kyverno.png`, `kyverno-terminal-ss.png`: Diagrams/screenshots for documentation.

## 🔄 Workflow

1. Push policy changes to GitHub.
2. Argo CD syncs the repo to your cluster.
3. Kyverno enforces the policy (audit or enforce mode).
4. Developers get instant feedback when creating Pods.

## 🚀 Quick Test

```bash
kubectl apply -f pod-with-no-resource-limit.yaml   # Should be blocked
kubectl apply -f pod-with-resource-limit.yaml      # Should be allowed
