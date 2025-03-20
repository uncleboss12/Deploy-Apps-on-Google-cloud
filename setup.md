### Deploy to App Engine
```bash
docker build -t test-python .

docker run --rm -p 8080:8080 test-python

gcloud app create --region=us-central

gcloud app deploy --version=one --quiet

gcloud app deploy --version=two --no-promote --quiet
```

### Deploy to Kubernetes Engine with Cloud Build and Artifact Registry
```bash
kubectl get nodes

gcloud artifacts repositories create devops-demo \
    --repository-format=docker \
    --location=us-central1

gcloud auth configure-docker us-central1-docker.pkg.dev


cd ~/gcp-course/deploying-apps-to-gcp
gcloud builds submit --tag us-central1-docker.pkg.dev/$DEVSHELL_PROJECT_ID/devops-demo/devops-image:v0.2 .


cd ~/gcp-course/deploying-apps-to-gcp
gcloud builds submit --tag us-central1-docker.pkg.dev/$DEVSHELL_PROJECT_ID/devops-demo/devops-image:v0.2 .


kubectl apply -f kubernetes-config.yaml

kubectl get pods

kubectl get services
```

## Deploy to Cloud Run
```bsah
cd ~/gcp-course/deploying-apps-to-gcp
gcloud builds submit --tag us-central1-docker.pkg.dev/$DEVSHELL_PROJECT_ID/devops-demo/cloud-run-image:v0.1 .
```
The rest is done in the UI
- When the build completes, on the Google Cloud console title bar, type Cloud Run in the Search field, then click Cloud Run in the Products & Pages section.

- Click Create service. This enables the Cloud Run API.

- Click the Select link in the Container image URL text box and then click Artifact Registry. In the resulting dialog, expand Region-docker.pkg.dev/$DEVSHELL_PROJECT_ID/devops-demo > cloud-run-image and select the image listed. Then click Select.

- In Service name, type hello-cloud-run and select region REGION.

- For Authentication, select Allow unauthenticated invocations.

- In Container(s), Volumes, Networking, Security, select Default in the Execution environment section.

- In Revision scaling, set the Maximum number of instances to 6. Leave the rest as defaults.

- Finally, click Create.
