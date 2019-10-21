# IAM Management

## Terminologies

### Roles

(RBAC) Role-based Access Control.

### Services Account

https://cloud.google.com/iam/docs/creating-managing-service-accounts

Every instances are attached one or more services accounts, and the instances could do what the services accounts allowed to do.



## Commands

List and Describe Roles

`````shell
gcloud iam roles list | grep "name:"
gcloud iam roles describe roles/compute.instanceAdmin
`````



Grant the role `roles/viewer` to the `$USERID2` within `$PROJECTID2`

`````shell
gcloud projects add-iam-policy-binding $PROJECTID2 --member user:$USERID2 --role=roles/viewer
`````



Create a role named `devops` and grant it appropriate permissions.

`````shell
gcloud iam roles create devops --project $PROJECTID2 --permissions "compute.instances.create,compute.instances.delete,compute.instances.start,compute.instances.stop,compute.instances.update,compute.disks.create,compute.subnetworks.use,compute.subnetworks.useExternalIp,compute.instances.setMetadata,compute.instances.setServiceAccount"
`````



Grant an user have permission to manage service accounts

````shell
gcloud projects add-iam-policy-binding $PROJECTID2 --member user:$USERID2 --role=roles/iam.serviceAccountUser
````



Create and list service accounts

````shell
gcloud iam service-accounts create devops --display-name devops
gcloud iam service-accounts list --filter "displayName=devops"
````



One liner to load the full email of a service account into environment variables.

`````shell
SA=$(gcloud iam service-accounts list --format="value(email)" --filter "displayName=devops")
`````

Create an instances attached with a service account.

`````shell
gcloud compute instances create lab-3 --service-account $SA --scopes "https://www.googleapis.com/auth/compute"
`````



Create key for services accounts

`````shell
gcloud iam service-accounts keys create ~/key.json \ --iam-account qwiklab@${PROJECT_ID}.iam.gserviceaccount.com
`````

Attached the key to your services accounts, thus enable the previous created instances to access certain APIs.

````shell
gcloud auth activate-service-account --key-file key.json
````



## Hand-on Labs

Configuring IAM Permissions with gcloud https://www.qwiklabs.com/focuses/7678 gives an good labs about iam accounts.

### Network Admin and Security Admin

- **Network Admin**: Permissions to create, modify, and delete networking resources, except for firewall rules and SSL certificates.
- **Security Admin**: Permissions to create, modify, and delete firewall rules and SSL certificates.

## Reference

* Configuring IAM Permission with gcloud https://google.qwiklabs.com/focuses/7678
* Network and Security Admin: https://www.qwiklabs.com/focuses/1231
* Service Accounts https://cloud.google.com/iam/docs/creating-managing-service-accounts

