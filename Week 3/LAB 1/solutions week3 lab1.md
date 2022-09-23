Working with IAM management console

Tasks

1. Login to your root account 
    After i logged into my root account
    I created three user groups and attached specified IAM users to the groups
2. Create an IAM group with S3 read only acess (S3 support).
    ![](solution%20week3%20lab1%20screenshots/s3%20support.png)

    ![](solution%20week3%20lab1%20screenshots/s3%20read%20only%20access.png)
3. Create an IAM group with EC2 read only acess (EC2 support)

    ![](solution%20week3%20lab1%20screenshots/ec2%20support.png)

    ![](solution%20week3%20lab1%20screenshots/ec2%20read%20only.png)
4. Create an IAM group with EC2 full access (EC2 admin)

    ![](solution%20week3%20lab1%20screenshots/ec2%20admin.png)

    ![](solution%20week3%20lab1%20screenshots/ec2%20full%20access.png)


    
5. Create 3 IAM users and add to the each group above as descibe below:
    
    user      group          permissions
    user1     EC2 support     Read-Only access to Amazon EC2
    user2     S3 support      Read-Only access to Amazon S3
    user3     EC2 admin       Full access to Amazon EC2 instances
    
    ![](solution%20week3%20lab1%20screenshots/usercreated.png)
    
    
    I created a policy to allow users to access AWS services, but only when they sign in with MFA.This policy also allows users to manage their own credentials on the My security credentials page

    ![](solution%20week3%20lab1%20screenshots/forcemfapolicy.png)

6. Test your design

    Logged into user1 console ![](solution%20week3%20lab1%20screenshots/testing%20user1%20login.png)

    I tried accessing ec2 service but got an error because I had not assigned MFA
    ![](solution%20week3%20lab1%20screenshots/error%20without%20mfa%20user1.png)

    After I assigned MFA for user1, I finally had access to EC2 console
    ![](solution%20week3%20lab1%20screenshots/access%20after%20mfa%20user1.png)

    I tested for the other users user2 and user3

7. Perform clean up operations


Replicate the process above for  Schulltech organization descrcibed below:


user           group                  permissions
adminstaff         EC2 support          Read-Only access to Amazon EC2
Techstaff          S3 support           Full access to S3
ITexpert           EC2/SDK admin        full access to EC2 and SDK
financialmanager     billingcontrol      Billing Full Access  
financeuser          billinguser          Billing view access

Created the groups mentioned above and granted them their respective permissions as mentioned above, I also added a policy to enforce mfa to the users in these groups
![](solution%20week3%20lab1%20screenshots/ec2support%20group.png)

![](solution%20week3%20lab1%20screenshots/s3supportgroup.png)

![](solution%20week3%20lab1%20screenshots/ec2adminsdk%20groups.png)

![](solution%20week3%20lab1%20screenshots/billingcontrolgroup.png)

![](solution%20week3%20lab1%20screenshots/billinguser%20group.png)

I created the users and added them to thier various groups.
![](solution%20week3%20lab1%20screenshots/techstaff%20user.png)

![](solution%20week3%20lab1%20screenshots/financialmanageruser.png)

![](solution%20week3%20lab1%20screenshots/financialuser.png)



I allowed programmatic access for the ITexpert to allow the user to have access to SDKs,because you can only access SDKs through access credentials
![](solution%20week3%20lab1%20screenshots/ITexpertuser.png)




