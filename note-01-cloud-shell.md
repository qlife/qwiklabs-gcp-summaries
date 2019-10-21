# Cloud Shell Setup

## Init

* https://cloud.google.com/sdk/gcloud/

`````shell
gcloud init

# Multiple projects configuration
gcloud config configurations create
`````



## Project Selection

```shell	
# Query
gcloud compute project-info describe --project <your_project_ID>
gcloud config list project

# Predefined Environ
echo ${GOOGLE_CLOUD_PROJECT}

# Load into Environment Variables
export PROJECT_ID=$(gcloud info --format='value(config.project)')

# Get project value only
gcloud config get-value core/project

gcloud config set project $PROJECT_ID2
```



## Zone Selection

Prepare an environ named `$ZONE` is much easier, as most of gcloud commands need an `--zone` parameters.

`````shell	
#export ZONE=<your_zone>
export ZONE=us-central1-a
gcloud config set compute/zone $ZONE
`````



## Get  User Email

`````shell
export USER_EMAIL=$(gcloud auth list --limit=1 2>/dev/null | grep '@' | awk '{print $2}')
`````



## How do I Get the IP Address of the Cloud Shell Instance?

`````shell
export ADDRESS=$(wget -qO - http://ipecho.net/plain)/32              # 32 is for the CIDR x.y.z.x/32
`````



## Finding Region of Cloud Shell Instance

`````shell
curl metadata/computeMetadata/v1/instance/zone
`````



## Cloud Shell Add-on

Finding all installed components

`````shell
gcloud components list
`````

Install components

```shell
gcloud components install beta
gcloud beta interactive
```

## Boost Mode, Web Preview, Safe Mode

* https://cloud.google.com/shell/docs/how-cloud-shell-works