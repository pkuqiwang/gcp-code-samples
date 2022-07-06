### Create a secret in Secret Manager
Check if Secret Manager is enabled, if not, enable secret manager.
```
gcloud services list --enabled | grep Secret
```
```
gcloud services enable secretmanager.googleapis.com
```

Then create a new secret in the Secret Manager
```
gcloud secrets create my-secret --replication-policy="automatic"
```
And add a secret to the secret
```
gcloud secrets versions add my-secret --data-file="./src/SecretManager/secret.txt"
```

Try access the secret
```
gcloud secrets versions access latest --secret=my-secret
```
