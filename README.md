# Sol9 GitOps Repository

This repository holds the Argo CD GitOps configuration for Sol9. The app repo
contains the Helm charts at `K8s/helm/*`, while this repo contains the Argo CD
Applications that reference those charts.

## Layout
- `argocd/`: AppProject + app-of-apps entrypoints (dev/staging/prod).
- `apps/dev/`: dev environment apps (Helm Applications).
- `apps/staging/`: staging environment apps (Helm Applications).
- `apps/prod/`: prod environment apps (Helm Applications).

## Quick start
1. Update repo URLs in:
   - `argocd/project.yaml`
   - `argocd/app-of-apps.yaml`
   - `argocd/app-of-apps-staging.yaml`
   - `argocd/app-of-apps-prod.yaml`
   - `apps/*/*.yaml`
2. Apply the GitOps bootstrap:
   ```bash
   kubectl apply -n argocd -f argocd/
   ```
3. In Argo CD, sync `sol9-apps`, `sol9-apps-staging`, and `sol9-apps-prod`.

## Notes
- The app-of-apps read `apps/<env>` and create the per-service Applications.
- The per-service Applications point to the app repo that hosts the charts.
- Postgres and Redis are shared infra per environment.
