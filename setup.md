docker build -t test-python .

docker run --rm -p 8080:8080 test-python

gcloud app create --region=us-central

gcloud app deploy --version=one --quiet

gcloud app deploy --version=two --no-promote --quiet


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


cd ~/gcp-course/deploying-apps-to-gcp
gcloud builds submit --tag us-central1-docker.pkg.dev/$DEVSHELL_PROJECT_ID/devops-demo/cloud-run-image:v0.1 .