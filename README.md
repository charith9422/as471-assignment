SSH Configure in Google Cloud
export PROJECT_ID='[thematic-metric-257605]'

gcloud iam service-accounts create ssh-account --project thematic-metric-257605 \
   --display-name "ssh-account"

gcloud compute networks create ssh-test --project thematic-metric-257605

gcloud compute firewall-rules create ssh-all --project thematic-metric-257605 \
   --network ssh-test --allow tcp:22

gcloud compute instances create target --project thematic-metric-257605 \
   --zone us-central1-f --network ssh-test \
   --no-service-account --no-scopes \
   --machine-type f1-micro --metadata=enable-oslogin=TRUE

gcloud compute instances add-iam-policy-binding target \
   --project thematic-metric-257605 --zone us-central1-f \
   --member serviceAccount:ssh-account@thematic-metric-257605.iam.gserviceaccount.com \
   --role roles/compute.osAdminLogin

gcloud compute instances create source \
   --project thematic-metric-257605 --zone us-central1-f \
   --service-account ssh-account@thematic-metric-257605.iam.gserviceaccount.com  \
   --scopes https://www.googleapis.com/auth/cloud-platform \
   --network ssh-test --machine-type f1-micro
Adding Docker
gcloud auth login

gcloud config set project thematic-metric-257605

#!/bin/sh
echo "Hello, world! The time is $(date)."

FROM alpine
COPY quickstart.sh /
CMD ["/quickstart.sh"]

gcloud builds submit --tag gcr.io/thematic-metric-257605/quickstart-image .


gcloud auth configure-docker

gcloud sql users set-password root \
    --host=% --instance=[INSTANCE_NAME] --prompt-for-password


SQL
gcloud config set project [PROJECT_ID]
gcloud config set compute/zone [ZONE]

Create a Compute Engine Instance
gcloud compute instances create mysql-test
gcloud compute ssh mysql-test

Install MySQL
sudo apt-get update
sudo apt-get -y install mysql-server
sudo mysql -u root -p