### Assignment 5
# Advanced GitOps Workflow with Kubernetes

## Objective

Extend your existing Kubernetes stack into a secure, multi-environment GitOps system using Flux CD or Argo CD. Incorporate environment-specific customization, encrypted secrets, and a robust CI pipeline to simulate real-world GitOps workflows.

This Assignment give you [10 Points] and potential [5 Bonus Points]. You need [6 Points] to pass this assignment

## Tasks

### 1. Deploy and Bootstrap a GitOps Operator (Flux or Argo CD) [2 Points]

Install and bootstrap a GitOps operator onto your Kubernetes cluster.

Requirements:
- Use Ansible to automate installation (optional challenge) [1 Bonus Point]
- Watch a separate Git repository for GitOps-controlled manifests (can be a new repo or a folder)
- Operator must:
  - Be deployed in its own namespace
  - Use a read-only Git deploy key
  - Reconcile at a regular interval

Deliverables:
- Ansible playbook (optional)
- Screenshot: Operator pod(s) running and reconciling
- Screenshot: GitHub repo showing reconciliation commit hash or status

### 2. Multi-Environment GitOps Setup with Kustomize or Argo CD Applications [2 Points]
Restructure your Kubernetes manifests to support multiple environments.

```
k8s/
├── base/                # Common base manifests
├── overlays/
│   ├── dev/             # Dev-specific customization
│   └── prod/            # Prod-specific customization
```

Requirements:
- Use Kustomize overlays (for Flux) or Application CRs (for Argo CD)
- Separate dev and prod with clear config differences (e.g., replica count, resources)
- Commit all manifests into Git so they can be applied by the operator

Deliverables:
- kustomization.yaml or Argo CD Application CR
- Screenshot: GitOps deployment successfully applied (e.g., app pod running via GitOps)
- Screenshot: Dev and prod services running with different settings

### 3. GitOps Secrets Management with Encryption [2 Points]

Use sealed-secrets or SOPS to securely manage secrets in Git.

Requirements:
- Store an encrypted Kubernetes Secret in Git
- Apply it automatically via GitOps
- Use a secret in the app (e.g., DB password, API key)

Hint: You could use a weather api that just prints out the current weather.

Deliverables:
- Encrypted YAML in Git
- Screenshot: Secret in cluster (kubectl get secret)

### 4. Secure GitOps Workflows and CI Pipeline [2 Points]

Expand your .github/workflows/ CI setup to include GitOps linting and PR gates.

Requirements:
- Run on PRs:
  - ansible-lint (if used)
  - kube-linter
- Block PRs with broken manifests
- Add a workflow that validates Kustomize build or Argo Application before merge

Deliverables:
- CI YAML workflows
- Screenshot: Green PR with all checks passing
- Screenshot: Failed PR due to linting issue

### 5. Self-Healing and Rollback Capability [2 Points]

Simulate failure and test GitOps system’s resilience.

Requirements:
- Delete a deployment or service manually
- Wait for GitOps to reconcile and restore it

Deliverables:
- Screenshot: Manual deletion
- Screenshot: Operator re-creating deleted resource

### Bonus (Optional for Extra Credit) [4 Points]

- Configure branch-based promotion (e.g., dev → staging → prod folder promotion) [2 Points]
- Add external secrets integration using external-secrets operator [2 Points]
