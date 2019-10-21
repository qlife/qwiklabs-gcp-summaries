# Cloud Storage and `gsutil`

## Basic Maneuver

### Create Bucket

`````shell
gsutil mb -c multi_regional -p ${PROJECTID} gs://${BUCKET}
`````

### Copy

* -m: enable multi threading mode
* cp -r : copy recursively

`````shell
gsutil -m cp -r endpointslambda gs://${BUCKET}
`````

## List Bucket

`````shell
gsutil ls gs://${BUCKET}/*
`````

### `Rsync`

* `-d`: delete remote if local not existed
* `-r`:  recursively

`````shell
gsutil -m rsync -d -r local_dirs gs://${BUCKET}/local_dirs
`````

## `ACL` Setting

`````shell
gsutil -m acl set -R -a public-read gs://${BUCKET}
`````

### Delete

`````shell
gsutil rm -rf gs://${BUCKET}/*
`````

### Delete Bucket

`````shell
gsutil rb gs://${BUCKET}
`````

## How to find Cloud Storage URL?

`````shell
http://storage.googleapis.com/<your-bucket-name>/*
`````



## Reference

* Using gsutil to Perform Operations on Buckets and Objects https://google.qwiklabs.com/focuses/7530

