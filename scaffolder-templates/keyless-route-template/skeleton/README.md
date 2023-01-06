# ${{values.component_id}}

${{values.description}}

## Deploying your API endpoint - Next Steps

Define the following argo application for this repository in `eks-cluster-automation`.

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: ${{values.component_id}}
  namespace: argo
spec:
  destination:
    namespace: ${{values.destination.owner}}
    server: https://kubernetes.default.svc
  project: ${{values.destination.owner}}
  source:
    path: helm/
    repoURL: git@github.com:MoveRDC/{{values.component_id}}.git
    targetRevision: sandbox
    helm:
      valueFiles:
        - values.yaml
        - values.sandbox.yaml
  syncPolicy:
    automated:
      selfHeal: true
      prune: true
    syncOptions:
      - CreateNamespace=true      
```
