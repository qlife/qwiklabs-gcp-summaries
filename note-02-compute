# Compute

## Compute Instances

`````shell
# describe
gcloud compute instances describe <your_vm>

# list
gcloud compute instances list

# ssh enter instances
gcloud compute ssh gcelab2 --zone $ZONE
`````

### Build Compute from Scratch

Combination: VPC -> subnet -> firewall-rules -> instances

`````shell
# Create a VPC `privatenet`, but will not create subnet in every available zone.
gcloud compute networks create privatenet --subnet-mode=custom

# Alternative: create VPC `auto-privatenet`.
gcloud compute networks create auto-privatenet --subnet-mode=auto

# Create VPC with specific region
# This 'private VPC' is used as a placeholder for creating a private GKE cluster
gcloud compute networks subnets create privatesubnet-us --network=privatenet --region=us-central1 --range=172.16.0.0/24

# Newly created VPC networks is unreachable until proper firewall-rules are created.
gcloud compute firewall-rules create [FIREWALL_NAME] --network privatenet --allow tcp,udp,icmp --source-ranges <IP_RANGE>
gcloud compute firewall-rules create [FIREWALL_NAME] --network privatenet --allow tcp:22,tcp:3389,icmp

gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0

# Create compute instances and appointed corresponding subnets
gcloud compute instances create privatenet-us-vm --zone=us-central1-c --machine-type=n1-standard-1 --subnet=privatesubnet-us
`````

### List Compute Resources

`````shell
# List all available compute instances, sorted by zone
gcloud compute instances list --sort-by=[ZONE]

# List VPC network
gcloud compute networks list

# List all subnet, sorted by VPC
gcloud compute networks subnets list --sort-by=[NETWORK]

# List all firewall-rules, sorted by VPC
gcloud compute firewall-rules list --sort-by=[NETWORK]
`````



### Cloud Disk

`````shell
# Create a cloud disk
gcloud compute disks create openarena-assets \ --size=50GB --type=pd-ssd\ --description="OpenArena data disk. Mount read-only at /usr/share/games/openarena/baseoa/" \ --zone ${zone_1}

# Attach the disk
gcloud compute instances attach-disk openarena-asset-builder \ --disk openarena-assets --zone ${zone_1}
`````



### Get Serial Output from Instances

When you'd like to read serial output from windows instances within the cloud shell

`````shell
gcloud compute instances get-serial-port-output $instance
`````



## Windows Specific

### How to Properly Reboot Your Windows Instances

* Restarting Windows Instances is quick
* `Stop Instances` is as long as a century



### Reset Windows Accounts Password

`````shell
gcloud compute reset-windows-password $windows-instance
gcloud beta compute --project [PROJECT_ID] reset-windows-password [WIN_INSTANCE] --zone [ZONE]
`````



### Connect to Windows Serial Port

https://cloud.google.com/compute/docs/instances/connecting-to-instance#windows

`````shell
# Enable Serial Port
gcloud compute instances add-metadata [INSTANCE_NAME] --metadata=serial-port-enable=1

# Connect
gcloud compute connect-to-serial-port [INSTANCE_NAME] --port=2
`````



## Transfer Files in between Instances

Best practices is ... _cloud storage_ ...

## Create a Container-Optimized OS Instance

 Firstly, finding the current available container OS images (`cos` images)

`````shell
gcloud compute images list \
    --project cos-cloud \
    --no-standard-images
`````

Create your instances now.

`````shell
 gcloud beta compute instances create-with-container containerized-vm2 \
     --image cos-stable-72-11316-136-0 \
     --image-project cos-cloud \
     --container-image nginx \
     --container-restart-policy always \
     --zone us-central1-a \
     --machine-type n1-standard-1
`````

Update the firewall rules:

`````shell
gcloud compute firewall-rules create allow-containerized-internal\
  --allow tcp:80 \
  --source-ranges 0.0.0.0/0 \
  --network default
`````

As we use `nginx` as an examples, the final checks is browse the website.

`````shell
http://[YOUR_EXTERNAL_IP_ADDRESS]
`````



## Cloud Functions

https://www.qwiklabs.com/focuses/916



## VPC Network Peering

Routing data in between different VPC network (could be two network in two different projects) https://www.qwiklabs.com/focuses/964



## Load Balancer

* L7 load balancer (AWS ELB like) https://www.qwiklabs.com/focuses/1232
* L3 load balancer (AWS NLB like), dispatching packets in between two different subnet in two different zones. https://www.qwiklabs.com/focuses/1250

## Reference

* Configure Network via gcloud https://www.qwiklabs.com/focuses/7140 
  * part of quest Using the Cloud SDK Command Line. https://google.qwiklabs.com/quests/95
* Container-Optimized OS https://www.qwiklabs.com/focuses/3414