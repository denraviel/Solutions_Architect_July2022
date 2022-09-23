1. Create a placement group
    
    I created a placement group with command:
        
    `aws ec2 create-placement-group --group-name lab-spread --strategy spread`  
    ![](Solutions%20week4lab3%20snaps/lab-spread%20create%20placement.png)
2. Tag a placement group
    
    `aws ec2 create-tags --resources pg-0a6ee870133a83bdb --tags Key=Cost-Centers,Value=SS-123`
    ![](Solutions%20week4lab3%20snaps/tagged%20to%20placement%20group.png)
3. Launch instances in a placement group
    `aws ec2 run-instances --image-id ami-05fa00d4c63e32376 --count 1 --key-name lab-key --security-group-ids sg-02c1d07d64b814405 --subnet-id subnet-05581a88586a0bda3 --placement "GroupName = lab-spread"`
    ![](Solutions%20week4lab3%20snaps/launched%20instance%20in%20lab-spread.png)
4. Describe instances in a placement group

    `aws ec2 describe-instances --instance-id i-0c74035106a1ec2e3`
    ![](Solutions%20week4lab3%20snaps/described%20instance%20for%20spread.png)
5. Change the placement group for an instance
   
    I created another placement group:
        `aws ec2 create-placement-group --group-name lab-spread2 --strategy spread`
        ![](Solutions%20week4lab3%20snaps/created%20lab-spread2%20placement%20group.png)
    
    To move the instance I stopped the instance:
        `aws ec2 stop-instances --instance-ids i-0c74035106a1ec2e3`
        ![](Solutions%20week4lab3%20snaps/stopped%20instance%20.png)
    
    I used the modify-instance-placement command to move instance from lab-spread to lab-spread2
        `aws ec2 modify-instance-placement --instance-id i-0c74035106a1ec2e3 --group-name lab-spread2`
        ![](Solutions%20week4lab3%20snaps/modified%20changes%20for%20labspread%201%202%20two.png)
    
    I restarted the instance:
        `aws ec2 start-instances --instance-ids i-0c74035106a1ec2e3`

6. Delete a placement group
    
    `
    `aws ec2 delete-placement-group --group-name lab-spread`
    `aws ec2 delete-placement-group --group-name lab-spread2`

    `aws ec2 terminate-instances --instance-ids i-0c74035106a1ec2e3`
    ![](Solutions%20week4lab3%20snaps/deleted.png)