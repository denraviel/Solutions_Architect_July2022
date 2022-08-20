 2. Launch a VPC with one public and one private subnets

 I created a VPC "my-demo-vpc" and created two subnets;one public and one private subnet
 ![](solution%20Images%20week%202%20lab%201/created%20my-demo-vpc%202.png)
 
 ![](solution%20Images%20week%202%20lab%201/created%20private%20and%20public%20subnets.png)

 3. Create two route table and associate  each one to each subnets
 
 I created two route tables,One for public subnet and one for private. I associated public route table to public subnet and private route table to private subnet
 
 ![](solution%20Images%20week%202%20lab%201/associate%20public%20subnet%20to%20public%20route%20table.png)
 
 
 ![](solution%20Images%20week%202%20lab%201/associate%20private%20route%20table%20to%20private%20subnet.png)
 4. Attach an internet gateway to the VPC and a NAT gateway to the private subnet
 
 I created an internet gateway and attached it to my custom VPC

![](solution%20Images%20week%202%20lab%201/created%20demo-internet-gateway%204.png) 

![](solution%20Images%20week%202%20lab%201/attached%20igw.png)
 
 Edited route for internet gateway to the public route table in the public subnet
 
 ![](solution%20Images%20week%202%20lab%201/edit%20route%20for%20internet%20gateway%20in%20public%20subnet.png)

 Created a Nat gateway in public subnet and allocated an elastic ip address
 ![](solution%20Images%20week%202%20lab%201/created%20natgateway%20in%20public%20subnet%20and%20allocated%20elastic%20ip.png)

 Edited route for Nat gateway to the private route table in the private subnet for intenet connectivity in the private subnet
 ![](solution%20Images%20week%202%20lab%201/edit%20route%20for%20natgateway%20in%20private%20subnet.png)

 5. Lauch a Linux instance into this VPC and attach the subnet

 Launched two instances, one in private subnet and another in public subnet
 ![](solution%20Images%20week%202%20lab%201/public%20and%20private%20instance.png)

 6. Test the network connectivity

 Testing network connectivity, I connected to the instance in public subnet first  
 ![](solution%20Images%20week%202%20lab%201/connect%20to%20public%20instance.png)
 
 Then connected to the instance in private subnet and tested internet connectivity.It had internet connection because of the Nat gateway placed in the public subnet
 ![](solution%20Images%20week%202%20lab%201/connecting%20to%20private%20instace%20through%20public%20instance.png)

 ![](solution%20Images%20week%202%20lab%201/had%20connection%20to%20internet%20through%20nat%20gateway%20in%20public%20subnet.png)