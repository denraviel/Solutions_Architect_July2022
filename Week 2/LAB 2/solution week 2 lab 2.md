1. Open your CLI and run a configuration setting

    I configured settings for cli 

2. Lauch a VPC

    Created a custom vpc with command `aws ec2 create-vpc --cidr-block 10.10.0.0/16`
    ![](solution%20images%20week%202%20lab%202/create%20vpc%20cli.png)

3. Create two subnets (a public and a private subnet)

    Created two subnets one public and the other private 
    
    `aws ec2 create-subnet --vpc-id vpc-027803c0173b3a632 --cidr-block 10.10.1.0/24 --tag-specifications ResourceType=subnet,Tags=[{key=Name,Value=public-subnet}]`

    ![](solution%20images%20week%202%20lab%202/created%20public%20subnet%20cli.png)

    `aws ec2 create-subnet --vpc-id vpc-027803c0173b3a632 --cidr-block 10.10.2.0/24 --tag-specifications ResourceType=subnet,Tags=[{key=Name,Value=private-subnet}]`
    ![](solution%20images%20week%202%20lab%202/create%20private%20subnet%20cli.png)

4. Make your subnet public by creating and attaching an internet gateway

    Created an internet gateway 
    `aws ec2 create-internet-gateway`
    ![](solution%20images%20week%202%20lab%202/create%20internet%20gateway.png)

    Attached internet gateway to vpc
    `aws ec2 attach-internet-gateway --vpc-id vpc-027803c0173b3a632 --internet-gateway-id igw-023f8a5b03e156977`
    ![](solution%20images%20week%202%20lab%202/attach%20internet%20gateway%20to%20vpc.png)

    Created a custom route table
    
    `aws ec2 create-route-table --vpc-id vpc-027803c0173b3a632 --tag-specifications ResourceType=route-table,Tags=[{key=Name,Value=route-table}]`
    ![](solution%20images%20week%202%20lab%202/created%20route%20table%20cli.png)

    Created a route in the route table that points all traffic (0.0.0.0/0) to the internet gateway using the following create-route command
    
    `aws ec2 create-route --route-table-id rtb-001f781cc97aa624a --destination-cidr-block 0.0.0.0/0 --gateway-id igw-023f8a5b03e156977`

   ![](solution%20images%20week%202%20lab%202/describe%20route.png) 

5. Create a security group and add a SSH access from anywhere
    Created a security group in my VPC 
    `aws ec2 create-security-group --group-name SSHAccess --description "for SSH access" --vpc-id vpc-027803c0173b3a632`
    ![](solution%20images%20week%202%20lab%202/created%20SG%20for%20ssh%20access.png)

    Added a rule that allows SSH access from anywhere using the authorize-security-group-ingress command
    `aws ec2 authorize-security-group-ingress --group-id sg-0da0c79a4b5ff3785 --protocol tcp --port 22 --cidr 0.0.0.0/0`
    ![](solution%20images%20week%202%20lab%202/SG%20group%20ingress.png)

    Configured subnet to issue a public IP to EC2 instances
    `aws ec2 modify-subnet-attribute --subnet-id subnet-0beeea3f2382c6bf4 --map-public-ip-on-launch`
    ![](solution%20images%20week%202%20lab%202/map%20public%20ip%20on%20launch.png)

6. Lauch an instance into your subnet 
    Launch instance in public subnet using security group and existing key pair
    `aws ec2 run-instances --image-id ami-090fa75a13c156b4 --count 1 --instance-type t2.micro --key-name rare --security-group-ids sg-0da0c79a4b5ff3785 --subnet-id subnet-0beeea3f2382c6bf4` 
    ![](solution%20images%20week%202%20lab%202/lauch%20instance%20in%20public%20subnet%20cli.png)

