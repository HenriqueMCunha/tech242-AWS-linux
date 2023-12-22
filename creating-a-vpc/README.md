# Creating a VPC

In order to create and set up a VPC there's a set of steps we need to follow:

1 - Create VPC

![Screenshot-create-vpc.png](../readme-images/Screenshot-create-vpc.png)

2 - Creating each of the subnets

![Screenshot-create-subnet-private.png](../readme-images/Screenshot-create-subnet-private.png)
![Screenshot-create-subnet-public.png](../readme-images/Screenshot-create-subnet-public.png)

3 - Create the internet gateway

![Screenshot-create-internet-gateway.png](../readme-images/Screenshot-create-internet-gateway.png)

 3a - Attach internet gateway to VPC

 ![Screenshot-attach-internet-gateway.png](../readme-images/Screenshot-attach-internet-gateway.png)

4 - Create Public Route Table

![Screenshot-create-public-route-table.png](../readme-images/Screenshot-create-public-route-table.png)

5 - Associate the public route table with the subnet

![Screenshot -associate-rt-to-public-subnet.png](<../readme-images/Screenshot -associate-rt-to-public-subnet.png>)

6 - Add internet gateway to the route

![Screenshot-add-internet-gateway-to-rt.png](../readme-images/Screenshot-add-internet-gateway-to-rt.png)

7 - Check to see if VPC is setup correctly

![Screenshot-test-vcp-setup.png](../readme-images/Screenshot-test-vcp-setup.png)

8 - Add database virtual machine to private subnet

    * The most important thing to remember is that a security group is specific to a VPC. That being the case, we cannot use a security group from a different VPC and will have to create our own.
    * Assign correct VPC.
    * Assign desired Subnet (private).
    * Disable public IP address.

![Screenshot-vpc-database-vm-security-group.png](../readme-images/Screenshot-vpc-database-vm-security-group.png)


9 - Add API virtual machine to public subnet

    * Like in the previous VM, we want to make sure the security group is associated to the same VPC.
      * Assign correct VPC.
      * Assign public Subnet.
      * Enable public IP address.
    * Additionally, we cannot forget to add the necessary piece of user data script.

![Screenshot-vpc-api-vm-security-group.png](../readme-images/Screenshot-vpc-api-vm-security-group.png)


10 - Check to see if api vm is accessed through internet

![Screenshot-step-10-vpc.png](readme-images/Screenshot-step-10-vpc.png)
