# ssg-workflows

Reusable GitHub Actions workflows for the SSG platform.

## Available workflows

| File | Trigger | Description |
|------|---------|-------------|
| `cloudrun-deploy.yml` | `workflow_call` | Go CI (vet + test) → deploy to GCP Cloud Run |
| `firebase-deploy.yml` | `workflow_call` | Build Vite → deploy **live** to Firebase Hosting |
| `firebase-preview.yml` | `workflow_call` | Build Vite → deploy **preview channel** to Firebase Hosting (posts link as PR comment) |

## Usage

### Cloud Run (Go services)

```yaml
jobs:
  deploy:
    uses: DaniFX/ssg-workflows/.github/workflows/cloudrun-deploy.yml@main
    with:
      service_name: ssg-my-service
      service_account_flag: --service-account=my-sa@project.iam.gserviceaccount.com
      ingress_flag: --ingress=internal-and-cloud-load-balancing
      env_vars: |
        ENV=production
        MY_VAR=${{ secrets.MY_VAR }}
    secrets: inherit
```

### Firebase Hosting — Live deploy

```yaml
jobs:
  deploy:
    uses: DaniFX/ssg-workflows/.github/workflows/firebase-deploy.yml@main
    with:
      project_id_secret: VITE_FIREBASE_PROJECT_ID
    secrets: inherit
```

### Firebase Hosting — Preview (PR)

```yaml
jobs:
  preview:
    uses: DaniFX/ssg-workflows/.github/workflows/firebase-preview.yml@main
    with:
      project_id_secret: VITE_FIREBASE_PROJECT_ID
    secrets: inherit
```
