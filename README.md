# Setting up an S3 bucket
 ## Connecting to AWS
- SSH into your machine
![image](https://user-images.githubusercontent.com/32297246/122209019-f32d0a00-ce9b-11eb-80e5-4f442c93df02.png)
- Install relevant dependancies:
```
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install python -y
sudo apt-get install python-pip -y
sudo apt-get install awscli -y
```
- run `aws configure`
![image](https://user-images.githubusercontent.com/32297246/122209662-ad247600-ce9c-11eb-8572-7feb3d98599a.png)
- enter the relevant info and DO NOT LEAK YOUR KEYS!
![image](https://user-images.githubusercontent.com/32297246/122209909-f5dc2f00-ce9c-11eb-918b-cf793f7c04fb.png)
- using `aws s3 ls` we can see all buckets and verify we are connected 
![image](https://user-images.githubusercontent.com/32297246/122210149-39cf3400-ce9d-11eb-9bc3-f94ca87c8467.png)

## Making the bucket
- To make a bucket, use `aws s3 mb s3://{name-of-bucket}`. 
- The name cannot contain `_`
![image](https://user-images.githubusercontent.com/32297246/122210677-cd086980-ce9d-11eb-90e8-824a44a7177b.png)
- use `aws s3 ls` again to verify creation
![image](https://user-images.githubusercontent.com/32297246/122210873-06d97000-ce9e-11eb-8427-0b6b3fe937ed.png)


## Placing a file in the bucket
- To copy a file to bucket, the command is `aws s3 cp {path to file} s3://{bucket name}/`
![image](https://user-images.githubusercontent.com/32297246/122211334-849d7b80-ce9e-11eb-916b-79954ced1b67.png)

## Making bucket access public
- To make the bucket contents public, on AWS got to the bucket's permissions and add the following to the bucket policy:
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::Bucket-Name/*"
            ]
        }
    ]
}
```
![image](https://user-images.githubusercontent.com/32297246/122220289-1958a700-cea8-11eb-84e1-1d195b291a70.png)

- The file is now accessible at https://devops-bootcamp-jack-bucket.s3.eu-west-1.amazonaws.com/testfile.txt

## Downloading from S3
 - To download the file off S3, use `aws s3 sync s3://{path to file on S3}`

## Removing the file from S3
- To remove the file, use `aws s3 rm s3://{path to file}`

## Deleting the bucket
- Buckets must be emptied before deletion
- `aws s3 rb s3://{name of bucket}`



