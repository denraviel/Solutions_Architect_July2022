1. Launch a non-default VPC

    I created a VPC with a 10.0.0.0/16 CIDR block and associated an IPv6 CIDR block with the VPC `aws ec2 create-vpc --cidr-block 10.0.0.0/16 --amazon-provided-ipv6-cidr-block`
    ![](solutions%20week%202%20lab3%20images/created%20vpc%20with%20ipv6%20.png)

2. Create two subnets 

    I created a public subnet with a 10.0.0.0/24 IPv4 CIDR block  
    `aws ec2 create-subnet --vpc-id vpc-071f231010cd1b591 --cidr-block 10.0.0.0/24 --ipv6-cidr-block 2600:1f18:250d:e200::/64`
    ![](solutions%20week%202%20lab3%20images/created%20public%20subnet%20ipv6.png)

    I created a private subnet with a 10.0.1.0/24 IPv4 CIDR block 

    `aws ec2 create-subnet --vpc-id vpc-071f231010cd1b591 --cidr-block 10.0.1.0/24 --ipv6-cidr-block 2600:1f18:250d:e201::/64`

    ![](solutions%20week%202%20lab3%20images/created%20private%20subnet%20ipv6.png)
3. Create an internet gateway to one of the subnets with route table

    I created an internet gateway using command `aws ec2 create-internet-gateway`
    ![](solutions%20week%202%20lab3%20images/created%20internet%20gateway%20.png)

    I attached internet gateway to my vpc
    `aws ec2 attach-internet-gateway --vpc-id vpc-071f231010cd1b591 --internet-gateway-id igw-055d00148b09ffa44`
 
    ![](solutions%20week%202%20lab3%20images/attach%20internet%20gateway%20to%20vpc.png)

    I created a custom route table for my public subnet 
    `aws ec2 create-route-table --vpc-id vpc-071f231010cd1b591`
    ![](solutions%20week%202%20lab3%20images/i%20created%20a%20custom%20route%20table%20for%20public%20subnet%20in%20vpc.png)

    I created a route in the route table that points all IPv6 traffic to the internet gateway `aws ec2 create-route --route-table-id rtb-0e7fc56e55b98475b --destination-ipv6-cidr-block ::/0 --gateway-id igw-055d00148b09ffa44`

    To confirm that my route has been created and is active, I used describe the route table and view the results
    `aws ec2 describe-route-tables --route-table-id rtb-0e7fc56e55b98475b`
    ![](solutions%20week%202%20lab3%20images/describe%20route%20for%20public%20route.png)

    I associated my public subnet to route table 
    `aws ec2 associate-route-table  --subnet-id subnet-08bb6e3a4a20a9f51 --route-table-id rtb-0e7fc56e55b98475b`
   ![](solutions%20week%202%20lab3%20images/associate%20route%20table%20to%20public%20subnet.png)
4. Configure an egress-only private subnet
    I created an egress-only internet gateway for my VPC
    `aws ec2 create-egress-only-internet-gateway --vpc-id vpc-071f231010cd1b591`
    ![](solutions%20week%202%20lab3%20images/created%20egress%20only%20internet%20gateway.png)

    I Created another custom route table for private subnet in my VPC
    `aws ec2 create-route-table --vpc-id vpc-071f231010cd1b591`
    ![](solutions%20week%202%20lab3%20images/created%20a%20custom%20route%20table%20for%20private%20subnet.png)

    I created a route in the route table that points all IPv6 traffic to the egress-only Internet gateway
    `aws ec2 create-route --route-table-id rtb-09e240053f85fbf82 --destination-ipv6-cidr-block ::/0 --gateway-id eigw-038bdeda73004c9b4`
   ![](solutions%20week%202%20lab3%20images/associated%20route%20private.png)
    I associated my private subnet to route table
    `aws ec2 associate-route-table  --subnet-id subnet-00e1e1a4985601786 --route-table-id rtb-09e240053f85fbf82`
    
    
5. Modify the IPv6 addressing behavior of the subnets
    
    I Modified the IPv6 addressing behavior of both subnets
    ![](solutions%20week%202%20lab3%20images/modified%20ipv6%20for%20both%20subnets.png)
6. Lauch an instance into your public subnet
    I created a security group to launch instance in public subnet
    `aws ec2 create-security-group --group-name SSHAccess --description "Security group for SSH access" --vpc-id vpc-071f231010cd1b591 `
    ![](solutions%20week%202%20lab3%20images/security%20group%20for%20public%20instance.png)

    I added a rule that allows SSH access from any IPv6 address using the authorize-security-group-ingress command
    ![](solutions%20week%202%20lab3%20images/authorize%20security%20group%20ingress%20to%20all%20ipv6.png)

    I launched an instance into my public subnet, using the security group and an already existing key pair that  created
    `aws ec2 run-instances --image-id ami-090fa75af13c156b4 --count 1 --instance-type t2.micro --key-name lab-key --security-group-ids sg-0161cfc4ac64740d8 --subnet-id subnet-08bb6e3a4a20a9f51`
    ![](solutions%20week%202%20lab3%20images/launch%20instance%20in%20public%20subnet.png)
7. Launch an instance into your private subnet
    I created a security group to launch instance in private subnet
    `aws ec2 create-security-group --group-name SSHAccessRestricted --description "SSH access from bastion" --vpc-id vpc-071f231010cd1b591`
    ![](solutions%20week%202%20lab3%20images/security%20group%20private%20imstance.png)
    I launched an instance into my private subnet, using the security group and an already existing key pair that  created

    `aws ec2 run-instances --image-id ami-090fa75af13c156b4 --count 1 --instance-type t2.micro --key-name lab-key --security-group-ids sg-02de3fb512a950337 --subnet-id subnet-00e1e1a4985601786`
    ![](solutions%20week%202%20lab3%20images/launched%20instance%20in%20private%20subnet.png)


8. Perform clean up operations.
    
    performed clean up operations by deleting resources