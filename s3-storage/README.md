# S3 Storage 

S3 Storage (or Amazon Simple Storage Service) is a scalable and highly durable object storage service provided by Amazon Web Services (AWS).  It is designed to store and retrieve any amount of data from anywhere on the web. S3 is commonly used for backup, archiving, content distribution, data storage for web applications, and more.

It is available globally and has a level of redundancy.

## Buckets

In Amazon S3, a bucket is a container for storing objects, which can consist of data files, images, videos, or any other type of data.

In Azure, it's called a container and it is for storing "blobs".

When you fist put an object in a bucket, they are not publicly accessible, that has to be defined in the scripts.

## Login in to AWS CLI

* First, we'll need to install and login to the AWS CLI (Amazon Web Services Command Line Interface):

`sudo apt install awscli -y`

* Verify it is installed:

`aws --version`

* Login to AWS CLI:

`aws configure` -> This will ask for Access Key ID and Secret Key.

 *It will also ask us for the default region name, which in our case is `eu-west-1` for Ireland.
 * It will also ask us for the default output format, which we'll want "json".

Once we're logged in, we'll be returned to the command line of our virtual machine.

## Create a bucket

### Gives list of buckets

`aws s3 ls`

### Get a help menu for AWS commands

`aws s3 help`

### Make bucket

`aws s3 mb s3://tech242-henrique-first-bucket `

### Check files in the specified bucket

`aws s3 ls s3://tech242-henrique-first-bucket `

### Output of this echo will redirect (>) to the test.txt file

`echo This is the first line in a test file > test.txt` 


### Copies/uploads the file into the bucket

`aws s3 cp test.txt s3://tech242-henrique-first-bucket`


### Download files from aws s3 bucket to current working directory 

`aws s3 sync s3://tech242-henrique-first-bucket .`


### Delete single file from s3 bucket

`aws s3 rm s3://tech242-henrique-first-bucket/test.txt`


### Delete all files fom s3 bucket (DANGEROUS)


`aws s3 rm s3://tech242-henrique-first-bucket --recursive`

### Remove bucket (cannot be done with objects inside)

`aws s3 rb s3://tech242-henrique-first-bucket`


### Remove bucket WITH ALL OBJECTS INSIDE (EXTREMELY DANGEROUS)

`aws s3 rb s3://tech242-henrique-first-bucket --force`






