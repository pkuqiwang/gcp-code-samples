# Workflow

This section will guide how to create a GCP Workflow using the resources created earlier.

### Enable Workflow
First, find out if Workflow is enabled in your project
```
gcloud services list --enabled | grep Workflow
```

You should see the followings if Workflow is enabled
```
workflowexecutions.googleapis.com    Workflow Executions API
workflows.googleapis.com             Workflows API
```

If not, use the following to enable Workflow
```
gcloud services enable workflows.googleapis.com
```

### Create Workflow service account

Create a service account for Workflow
```
export SERVICE_ACCOUNT=workflows-sa
export PROJECT_ID=$(gcloud config get-value project)

gcloud iam service-accounts create ${SERVICE_ACCOUNT} --display-name="Worflow Service Account for sample"

gcloud projects add-iam-policy-binding $PROJECT_ID \
    --member "serviceAccount:${SERVICE_ACCOUNT}@${PROJECT_ID}.iam.gserviceaccount.com" \
    --role "roles/run.invoker"
```

### Create Workflow

```
gcloud workflows deploy myWorkflow \
    --source=myWorkflow.ymal \
    --service-account=sa-name@PROJECT_ID.iam.gserviceaccount.com
```

