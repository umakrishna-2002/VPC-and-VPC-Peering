# VPC-and-VPC-Peering
Creating a VPC's establishing connection between tow private subnets of two different VPC's using Peering connection.
![image](https://github.com/user-attachments/assets/9d65ee39-f56e-4ee4-a29e-65b76a20807d)

Creating a VPC that consist  Subnets with 5 subnets in it, with one public subnet and leaving rest as private.

Second VPC with two subnets with one as private and one as public subnets.

Creation of production VPC:

![image](https://github.com/user-attachments/assets/31e15ce5-8a43-4a1e-a691-3b901f146efc)

Now create subnets names
1. App1
2. App2
3. DB
4. DBcache
5. Web

NOTE: All the subnets are private by default.

![image](https://github.com/user-attachments/assets/d04898e6-af3a-40b6-88eb-106e612e7f06)


Create an Internet Gateway to access the internet through a public subnet and add production vpc to it.

![image](https://github.com/user-attachments/assets/43052afb-1d69-4806-96b5-77b64febb75d)

Create a Route Table to add a public subnet and Internet gateway. 

Public subnet is associated with the public route table.

![image](https://github.com/user-attachments/assets/67ab7025-5c48-47c0-8c58-a54d4a8e9b23)

Now add the Intenet Gateway which is created tot he Route Table.

![image](https://github.com/user-attachments/assets/fe506c4a-6cb5-4d3d-a75f-3467899848c9)

Create another route table to associate private subnets.

![image](https://github.com/user-attachments/assets/ecb40c3b-e9bb-4c16-b73f-9d3f383a39b2)

App1 and DBcache instances are associated to the private route table. As they are private subnets and need to send the internet request.

![image](https://github.com/user-attachments/assets/a4ef3348-bf37-486a-81bc-497e40819c37)

Create a NAT gateway and add it to the private route table.

![image](https://github.com/user-attachments/assets/8e44afb1-6719-4f74-8198-cf1f01124ed2)

Now add the NAT gateway to the Route Table to which we attached the Private Subnets.

![image](https://github.com/user-attachments/assets/5b517e03-a225-49e1-894b-d71dd171a7a8)

Production VPC is created.

![image](https://github.com/user-attachments/assets/afb9f9c4-5b5c-4db5-a388-588521338c1e)

Now we need to create Development VPC.

![image](https://github.com/user-attachments/assets/92074395-4853-4233-97aa-81559dba36bc)

Two SUbnets were created.
1. DB
2. Web

![image](https://github.com/user-attachments/assets/94006fa6-368e-4fbb-a793-07bd2f0ca6c8)

Create a Route Table to add public subnet to it.

![image](https://github.com/user-attachments/assets/a28775d6-98a3-4698-b05d-a8a2c29b0f54)

Now create an Internet Gateway and add it to the Route Tavle to which we added public subnet to it, which will access the internet.

![image](https://github.com/user-attachments/assets/6075dc24-f283-466c-92fb-56361500b1b6)

Development VPC is created with two subnets, one private and one public.

![image](https://github.com/user-attachments/assets/a62b3cfe-d538-42de-a1bf-217f93073d7f)

We need to create EC2 instances to access the VPC's created. 

EC2 instances for Production VPC.

NOTE: Here we can only access the instance with Public Subnet (Web) of production VPC associated with it.
![image](https://github.com/user-attachments/assets/6bca2210-3eb8-4dde-b8b8-62654674e2fd)

Connect to  public subnet instance which prod-web and check for intent connectivity.

Checking the internet connectivity.
![image](https://github.com/user-attachments/assets/df8242cb-07c4-4802-b29e-e05de60715ae)

Connect to APP1 instance through Web instance, through the private IP address of APP1 instance.

![image](https://github.com/user-attachments/assets/9834abbf-5377-4b4f-bc1d-2186616979ff)

Now you can access the internet through the private instances, which is connected through public instance.

![image](https://github.com/user-attachments/assets/bb2bb77c-a35d-4e42-baa4-e4f06ac8934f)

Connecting to DBcahce of Production through public Web instance.

![image](https://github.com/user-attachments/assets/957daccf-4420-44aa-a8cf-46da3bce07dc)

Now creating EC2 instance for Development VPC

1. One with private subnet and other with private subnet.
2. Here Web is public subnet, through which we are going to access the internet.

![image](https://github.com/user-attachments/assets/cdac4266-cbe8-4ad1-8588-5c5fd9692757)


Connect Development web instance which has public access. 

![image](https://github.com/user-attachments/assets/4e77f6e6-dabd-46be-a114-dd0740eb5bb7)


Now we need to make VPC peering between Production VPC and Development VPC.

Naviagte to Peering section in VPC.

Create a Peering with Development-VPC as Requestor and Production VPC as Acceptor.

![image](https://github.com/user-attachments/assets/d2f6cfa5-0334-4c39-9391-1e1947f868e1)


Go to the default Route Table which is created for Proudction VPC and add CIDR of DB subnet of Development VPC.

![image](https://github.com/user-attachments/assets/ba5f68ba-4af0-48de-a273-005bd47def74)
![image](https://github.com/user-attachments/assets/654216f7-2989-4bbf-9d6a-f795efcdcc44)

Similarly, for Development VPC add the DB subnet CIDR in the default Route Table.

![image](https://github.com/user-attachments/assets/dbc906dc-d01a-4201-9ce2-a36d856cbc30)


Connecting to Development DB instance from Production DB instance.

Try to access the DB instances of Development instances through it's private IP address.

![image](https://github.com/user-attachments/assets/6706e505-9d28-43d4-9a59-3f2d0d9906c5)

Hence,
1. Production VPC is created with one public subnet and 4 private subnets and accessed the private subnet instances through public subnet instance.
2. Development VPC is created with  public subnet, private subnet each and accessed the private subnet instance through public subnet instance.
3. VPC peering between two VPC's and connection is established between both DB subnets of Production and Development VPC.

