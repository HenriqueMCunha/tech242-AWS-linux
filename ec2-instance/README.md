# How to Create an EC2 Instance

Before creating Instance, make sure I am in Ireland Zone.

### 1. Create Instance

Assign a descriptive name to the instance.

![Screenshot-ec2-name.png](../readme-images/Screenshot-ec2-name.png)

### 2. Select AMI

To find Ubuntu Bionic 18.04, we need to search for the date in which it was released: 20230424 in the Community AMIs section.
Every base image has an AMI Id for it, in this case we have to find one that finishes in "1e9".

![Screenshot-ec2-select-ami.png](../readme-images/Screenshot-ec2-select-ami.png)

Select free instance type (t2.micro).

![Screenshot-ec2-instance-type.png](../readme-images/Screenshot-ec2-instance-type.png)

### 3. Choose a key pair 

Selected Key pair supplied to us from Ramon. (Add definition of key pair)
Saved the key in appropriate location.

![Screenshot-ec2-key-pair.png](../readme-images/Screenshot-ec2-key-pair.png)

### 4. Create own Security Group

Give it the same initial part of name we gave to instance and keep description clear with what we want in our security group.
Allow for SSH only from our current IP address.
Allow for HTTP from anywhere.

![Screenshot-ec2-security-group.png](../readme-images/Screenshot-ec2-security-group.png)

### 5. Double check everything we selected

### 6. Launch the instance

### 7. Connect to the instance

Press Connect - then go to SSH client.

![Screenshot-ec2-connect.png](../readme-images/Screenshot-ec2-connect.png)

Make sure the key pair required is in the designated folder.

Connected to instance by using GitBash, by specifying the public address of our instance, the username and the private key that was given to us to create the instance.

Make sure you connect to the instance whilst being in the folder where your key is in.
* We can also circunvent this if we are in a different directory by adding our desired path to the command given in the connect to instance section:
* Original command: `ssh -i "tech242.pem" ubuntu@ec2-18-202-81-78.eu-west-1.compute.amazonaws.com`
* With desired path: `ssh -i "~/.ssh/tech242.pem" ubuntu@ec2-18-202-81-78.eu-west-1.compute.amazonaws.com`


![Virtual Machine Diagram.png](<../readme-images/Virtual Machine Diagram.png>)


