## SETUP

```
gcloud config set project <PROJECT ID>

export PROJECT_ID=$(gcloud config get project)
export PROJECT_NUMBER=$(gcloud projects describe $PROJECT_ID --format="value(projectNumber)")
```

### WORKLOAD IDENTITY PERMISSION FOR SA 

```
SERVICE_ACCOUNT_EMAIL="github@coursebox-ai-dev.iam.gserviceaccount.com"
WORKLOAD_IDENTITY_POOL_ID="github"
WORKLOAD_IDENTITY_PROVIDER_ID="github"
GITHUB_REPO="demo-flask-app"

gcloud iam service-accounts add-iam-policy-binding $SERVICE_ACCOUNT_EMAIL \
  --role="roles/iam.workloadIdentityUser" \
  --member="principalSet://iam.googleapis.com/projects/$PROJECT_NUMBER/locations/global/workloadIdentityPools/$WORKLOAD_IDENTITY_POOL_ID/attribute.repository/$GITHUB_REPO"
```