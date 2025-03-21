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


# Monitoring Applications in Google Cloud
```bash
gcloud auth list

gcloud config list project

gcloud config set project [PROJECT_ID]

mkdir gcp-logging

cd gcp-logging

git clone https://GitHub.com/GoogleCloudPlatform/training-data-analyst.git

cd training-data-analyst/courses/design-process/deploying-apps-to-gcp
```
open editor `import googlecloudprofiler


try:
    googlecloudprofiler.start(verbose=3)
except (ValueError, NotImplementedError) as exc:
    print(exc)`

add in the requirements.txt
`google-cloud-profiler==3.0.6
protobuf==3.20.1`


```
bashg
cloud services enable cloudprofiler.googleapis.com```
```bash
docker build -t test-python .

docker run --rm -p 8080:8080 test-python
```
to use app engine create a file called app.yaml then put
`runtime: python39`

save and run
```bash
gcloud app create --region=asia-east1

gcloud app deploy --version=one --quiet```


- On the Google Cloud console title bar, type App Engine in the Search field, then click App Engine in the Products & Pages section.

- Click App Engine > Dashboard. The upper-right corner of the dashboard should display a link to your application similar to this:
__Note: By default, the URL to an App Engine instance is in the form of https://project-id/appspot.com.__
- Click on the link to test your program.

- Refresh your browser a few times to make some requests.

- Return to the Console and click the App Engine > Versions.

- In Diagnose column of the table click Logs.

- The logs should indicate that Profiler has started and profiles are being generated. If you get to this point too quickly, wait a minute and click Refresh.

### Inside an instance, run this below:
```bash
sudo apt update
sudo apt install apache2-utils -y
```

- after run this to populate the app.engine so we can view the logs in the **profiler** on google cloud
```bash
ab -n 1000 -c 10 https://<your-project-id>.appspot.com/
```
now do same, using the same command in the instance then open **Trace Explorer**

then go to cloud monitoring to check.
