1. Create an Amazon EBS volume
    
    `aws ec2 create-volume --volume-type gp2 --size 8 --availability-zone us-east-1a`
    ![](solution%20week%204%20lab%202%20screens/create%20ebs.png)

2. Attach and mount your volume to an EC2 instance
    
    `aws ec2 attach-volume --volume-id vol-03aecc336deaef9c5 --instance-id i-02e42f316d16d6106 --device /dev/sdf`
    ![](solution%20week%204%20lab%202%20screens/attach%20ebs%20to%20instance.png)

3. Create a snapshot of your volume
    
    `aws ec2 create-snapshot --volume-id vol-03aecc336deaef9c5 --description "This is my volume snapshot"`
    ![](solution%20week%204%20lab%202%20screens/snapshot%20of%20my%20ebs%20volume%20.png)

4. Create a new volume from your snapshot
    
    `aws ec2 create-volume --volume-type gp2  --snapshot-id snap-0b9e6062e7bd07938 --availability-zone us-east-1a`
    ![](solution%20week%204%20lab%202%20screens/create%20ebs%20volume%20with%20snapshot%20id.png)

5. Attach and mount the new volume to your EC2 instance
    
    `aws ec2 attach-volume --volume-id vol-0a1bdfcd1e6614451 --instance-id i-02e42f316d16d6106 --device xvdh`
    ![](solution%20week%204%20lab%202%20screens/attach%202nd%20volume%20to%20instance.png)

Performed clean up
    `aws ec2 detach-volume --volume-id vol-0a1bdfcd1e6614451`
    ![](solution%20week%204%20lab%202%20screens/detach1.png)
    `aws ec2 detach-volume --volume-id vol-03aecc336deaef9c5`
    ![](solution%20week%204%20lab%202%20screens/detach2.png)
    `aws ec2 delete-volume --volume-id vol-0a1bdfcd1e6614451`
    `aws ec2 delete-volume --volume-id vol-03aecc336deaef9c5`
    ![](solution%20week%204%20lab%202%20screens/deleted.png)