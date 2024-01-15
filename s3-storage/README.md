# S3 Storage 

- [S3 Storage](#s3-storage)
    - [It is available globally and has a level of redundancy:](#it-is-available-globally-and-has-a-level-of-redundancy)
    - [It also provides High Availability:](#it-also-provides-high-availability)
    - [How S3 Storage helps in disaster recovery:](#how-s3-storage-helps-in-disaster-recovery)
  - [Buckets](#buckets)
  - [Login in to AWS CLI](#login-in-to-aws-cli)
  - [Create a bucket](#create-a-bucket)
    - [Gives list of buckets](#gives-list-of-buckets)
    - [Get a help menu for AWS commands](#get-a-help-menu-for-aws-commands)
    - [Make bucket](#make-bucket)
    - [Check files in the specified bucket](#check-files-in-the-specified-bucket)
    - [Output of this echo will redirect (\>) to the test.txt file](#output-of-this-echo-will-redirect--to-the-testtxt-file)
    - [Copies/uploads the file into the bucket](#copiesuploads-the-file-into-the-bucket)
    - [Download files from aws s3 bucket to current working directory](#download-files-from-aws-s3-bucket-to-current-working-directory)
    - [Delete single file from s3 bucket](#delete-single-file-from-s3-bucket)
    - [Delete all files fom s3 bucket (DANGEROUS)](#delete-all-files-fom-s3-bucket-dangerous)
    - [Remove bucket (cannot be done with objects inside)](#remove-bucket-cannot-be-done-with-objects-inside)
    - [Remove bucket WITH ALL OBJECTS INSIDE (EXTREMELY DANGEROUS)](#remove-bucket-with-all-objects-inside-extremely-dangerous)


S3 Storage (or Amazon Simple Storage Service) is a scalable and highly durable object storage service provided by Amazon Web Services (AWS).  It is designed to store and retrieve any amount of data from anywhere on the web. S3 is commonly used for backup, archiving, content distribution, data storage for web applications, and more.

### It is available globally and has a level of redundancy:
 * S3 stores data across multiple devices at geographically dispersed locations within an Availability Zone (AZ). This means an entire AZ needs to be down for data to be lost. Even within an AZ, data is spread across multiple devices, further bolstering redundancy.
 * For extra protection, an user can opt to store data across multiple AZs within a Region. This ensures data remains accessible even if an entire AZ experiences an outage.
 * S3 regularly verifies the integrity of data using checksums. This detects any corruption and triggers automatic repairs, ensuring data consistency.
 * A checksum is a small piece of data, typically a string of letters and numbers, that acts as a unique fingerprint for a larger block of data like a file or a message. It's used to verify the integrity of the data, meaning it helps ensure that the data hasn't been corrupted or altered in any way during transmission or storage.

### It also provides High Availability:
 * S3's distributed architecture enables it to automatically adapt to hardware failures without impacting data access. If a device fails, data remains accessible on other devices.
 * S3 allows users to easily scale their storage capacity on demand. This ensures user's applications can access data quickly and efficiently even as their data volume grows.
 * AWS has a global network of Regions and AZs, providing low latency access to user's data from anywhere in the world.

### How S3 Storage helps in disaster recovery:
 * S3 Storage allows for S3 Replication. This means that users can replicate their data to another S3 Bucket in a different Region. This creates a geographically separate copy of the user's data, which can prove invaluable in case of a regional disaster.
 * For long-term archival needs, Glacier Deep Archive offers extremely durable storage at a very low cost. This is ideal for disaster recovery purposes, as it ensures user's data can be retrieved even if their primary storage is unavailable.
 * S3 also allows users to enable versioning, which keeps previous versions of their data even after they overwrite it. This provides a safety net in case of accidental deletion or corruption.



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






