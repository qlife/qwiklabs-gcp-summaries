# Cloud SQL

## Setup Cloud SQL Instances

### Create

`````shell
gcloud sql instances create flights \ --tier=db-n1-standard-1 --activation-policy=ALWAYS
`````

### Root DB Password

`````shell
gcloud sql users set-password root --host % --instance flights \ --password Passw0rd
`````

## Whistling

Cloud SQL put restriction on the IP may connect with.

Whistling is a temporary solution. 

`````shell
export ADDRESS=$(wget -qO - http://ipecho.net/plain)/32
gcloud sql instances patch flights --authorized-networks $ADDRESS
MYSQLIP=$(gcloud sql instances describe \ flights --format="value(ipAddresses.ipAddress)")
`````

### Cloud SQL Proxy

Formal approach to maintain a secure SQL connection.

Download Cloud SQL Proxy

`````shell
wget https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 -O cloud_sql_proxy
`````

Configure the file mode

`````shell
chmod +x cloud_sql_proxy
`````

Connect with Unix socket

````shell
# Create SQL Proxy
./cloud_sql_proxy -dir=/cloudsql -instances=myProject:us-central1:myInstance,myProject:us-central1:myInstance2 

# Use mysql to connect DB
mysql -u myUser -S /cloudsql/myProject:us-central1:myInstance2
````

## Upload Data

Note that you may import CSV into newly created Cloud SQL instances, see the lab https://www.qwiklabs.com/focuses/2802

## Reference

* CloudSQL with Terraform https://www.qwiklabs.com/focuses/1215?parent=catalog : provide good introduction about `terraform` and `cloud SQL proxy`
* Using Ruby on Rails with Cloud SQL for PostgreSQL https://www.qwiklabs.com/focuses/1854?parent=catalog

* Data Science on GCP https://github.com/GoogleCloudPlatform/data-science-on-gcp/