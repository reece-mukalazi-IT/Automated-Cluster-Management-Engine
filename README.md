
# Automated Cluster Management Engine

A custom Kubernetes controller that watches your own Custom Resource 
Definitions (CRDs) — such as `AppEnvironment` — and continuously 
reconciles cluster state to match your declared intent. 

I will also be self hosting this project, relying on my own personal hardware and utilising systems like proxmox to make this possible.

This is how the Automated Cluster Management Engine queuing system will work:

<img width="770" height="455" alt="image" src="https://github.com/user-attachments/assets/9aad3e5b-c57d-485a-8cfc-1463a92129b1" />

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

  ## Use Cases for the Automated Cluster Management Engine

How will the Kubernetes API server Store CRD changes ?

When creating cutome resources such as 'App Enviroment', the API server will push it through a well defined pipeline the etcd:

The first step will be the Admission chain:

- First step will be mutating admission webhooks will be able to modify the object such as injecting default fields and values adding default labels. This will be running first so that validators can see the final shape.

- Secondly validating webhooks this can only approve or reject. THis is where I will enforce buisness rules like "env must be apart of the staging/production process.

These will be defined as `MutatingWebhookConfiguration` and `ValidatingWebhookConfiguration` resources.
  
