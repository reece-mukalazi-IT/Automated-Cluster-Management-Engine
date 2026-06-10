<img width="574" height="97" alt="image" src="https://github.com/user-attachments/assets/3b42e332-5819-43ae-a1f6-71143ee449e4" />

# Automated Cluster Management Engine

A custom Kubernetes controller that watches your own Custom Resource 
Definitions (CRDs) — such as `AppEnvironment` — and continuously 
reconciles cluster state to match your declared intent. Define your 
environments in YAML; the engine handles the rest.

## What it does

Rather than imperatively scripting cluster changes, you declare what 
you want via custom resources. The controller's reconciliation loop 
detects drift between desired and actual state and corrects it 
automatically — including provisioning Deployments, Services, 
ConfigMaps, and HPAs based on a single `AppEnvironment` spec.

## Key concepts

- **Custom Resource Definitions** — `AppEnvironment` and other CRDs 
  act as the API surface for your cluster automation
- **Reconciliation loop** — watch → queue → reconcile → observe, 
  repeated continuously
- **Declarative by default** — idempotent controllers that converge 
  to desired state regardless of how many times they run
- **Extensible architecture** — new CRD handlers can be wired in 
  without touching the core controller machinery
