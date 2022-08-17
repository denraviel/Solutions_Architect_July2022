Logged into aws account using aws cli


Create a S3 bucket
I created s3 bucket with command `aws s3 mb s3://denraviel-bucket`
![](Solution%20lab1%20week%201%20images/create%20S3bucket.png)
Created a folder "new-folder in bucket and uploaded a jpg file into the folder in s3 bucket
`aws s3 cp rave.jpg s3://denraviel-bucket/new-folder/rave`

List the object in your S3 bucket
To list object in s3 bucket I used command 
`aws s3 ls s3://denraviel-bucket/new-folder/`

Download Object from your S3 bucket
`aws s3api get-object --bucket denraviel-bucket --key new-folder/rave ravedownload.jpeg --output json`

Delete object in your s3 bucket
`aws s3 rm s3://denraviel-bucket/new-folder/rave`

Delete your S3 bucket
`aws s3 rb s3://denraviel-bucket --force`