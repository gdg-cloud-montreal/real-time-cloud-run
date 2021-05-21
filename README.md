# real-time-cloud-run

1. Ensure that gcloud is currently configured to your desired project

```
gcloud config get-value project
```

2. If not, set it with:

```
gcloud config set project <project-id>
```


3. Build the custom image:


```
gsutil cp gs://demo2020-workspace-tools/cloudbuild.yaml .
gcloud builds submit --no-source --substitutions _DEMO_USER=$(whoami)
```

4. Deploy to Cloud Run:

```
gcloud run services replace jfrog-service.yaml --region=us-central1 --platform=managed
```

5. Allow all traffic to service (demo)

```
gcloud run services set-iam-policy jfrog-service policy.yaml --region=us-central1 --platform=managed
``` 


or
```
gcloud run services add-iam-policy-binding jfrog-service --member="allUsers" --role="roles/run.invoker" --region=us-central1 --platform=managed
``` 