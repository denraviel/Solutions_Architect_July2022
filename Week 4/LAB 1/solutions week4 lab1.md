# Working with EC2 instance using the AWS CLI / Programmable access

Tasks:

1. Using your default vpc, find the public subnet
    I logged into my aws account using Programmable access(command line interface)

    I checked the public subnet in my default vpc 
    

    `aws ec2 describe-vpcs`
    ![](Solution%20week%204%20screens/describe%20vpc.png)
    
    `aws ec2 describe-subnets --filter Name=vpc-id,Values=vpc-095d30e35e066f00b`
    ![](Solution%20week%204%20screens/describe%20subnets.png)
    


2. Create a security group
   

    I created a security group:
     
    `aws ec2 create-security-group --group-name MySecurityGroupDemo --description "My security group" --vpc-id vpc-095d30e35e066f00b`
    ![](Solution%20week%204%20screens/created%20security%20group%20for%20instance.png)

    To permit inbound traffic from my ip address on port 22, enable SSH in the same security group : 
    
    `aws ec2 authorize-security-group-ingress --group-id sg-02c1d07d64b814405 --protocol tcp --port 22 --cidr 197.210.52.26/24`
    ![](Solution%20week%204%20screens/authorize%20security%20group%20ingress%20port%2022.png)


3. Launch an instance with a web server with termination protection enabled
    I wrote a script to launch an instance with apache web server 

    `aws ec2 run-instances --image-id ami-05fa00d4c63e32376 --count 1 --instance-type t2.micro --key-name lab-key --security-group-ids sg-02c1d07d64b814405 --subnet-id subnet-05581a88586a0bda3 --user-data file://"C:\Users\denra\Downloads\my_script.sh"`
    ![](Solution%20week%204%20screens/launched%20instance%20with%20script.png)
    
    
    
    

    The DisableApiTermination attribute controls whether the instance can be terminated using the console, CLI, or API. I used the `modify-instance-attribute` command to enable termination protection :
        `aws ec2 modify-instance-attribute --disable-api-termination  --instance-id i-0fb6d9b5878a00846`
        ![](Solution%20week%204%20screens/modified%20instance%20attribute%20disable%20termination%20protection.png)
        ![](Solution%20week%204%20screens/enabled%20protection.png)

     

4. Monitor Your EC2 instance; view the types of metrics that are collected for an EC2 instance
    To monitor my instance I used the `monitor-instances` command:
        `aws ec2 monitor-instances --instance-ids i-0fb6d9b5878a00846`
        ![](Solution%20week%204%20screens/monitor%20instance.png)
        
    To view the type of metrics collecte on instance I used the `aws cloudwatch list-metrics`command: 
        
    `aws cloudwatch list-metrics --namespace AWS/EC2 --dimensions Name=InstanceId,Value=i-0fb6d9b5878a00846`
    ![](Solution%20week%204%20screens/monitor%20metrics.png)

5. Modify the security group that your web server is using to allow HTTP access
    
    The following command will add a rule for HTTP (port 80) access with the security ID group sg-02c1d07d64b814405. To allow access for all:
        `aws ec2 authorize-security-group-ingress --group-id sg-02c1d07d64b814405 --protocol tcp --port 80 --cidr 0.0.0.0/0`
        ![](Solution%20week%204%20screens/http%20authorize%20sec%20group%20ingress.png)

        I checked the test page with the public address to confirm the script worked
        http://public ip
        ![](Solution%20week%204%20screens/test%20page%20apache.png)

6. Resize your Amazon EC2 instance to scale
    To resize Amazon Ec2 instance the instance must be stopped state

    To put instance on stopped state :`aws ec2 stop-instances --instance-ids i-0fb6d9b5878a00846`
    ![](Solution%20week%204%20screens/stopped%20state%20instance.png)

    To resize Amazon EC2 instance to scale I used command:
    `aws ec2 modify-instance-attribute --instance-id i-0fb6d9b5878a00846 --instance-type "{\"Value\": \"m1.small\"}"`
    ![](Solution%20week%204%20screens/modified%20instance%20m1small.png)
    
    ![](Solution%20week%204%20screens/confirm%20instance%20type%20change.png)

    