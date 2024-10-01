<h2 align="center"> VPC PEERING CONNECTION</h2>

This project demonstrates how to carry out a VPC Peering connection between two VPCs. A VPC Peering connection is a networking peering connection that allows resources within two or more separate VPCs to easily communicate as if they were in the same network. It enables instances in either VPC to communicate with each other using private IP addresses without the data traversing the Internet. It stays within the AWS network.

<h3 align="left"> Case Study</h3>

Suppose a company after experiencing a lot of growth decides to host all their application servers in one VPC and database servers in another VPC. To enable effortless communication, a VPC Peering connection would have to be created that would allow both VPCs to communicate effortlessly. One advantage of this type of connection is privacy as all communications are carried out within the AWS Network.


<p align="center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/network-architecture.png" height="55%" width="75%"/>
</p>


<h3 align="left"> Creating The VPCs</h3>

The first step is to create both VPCs, VPC-Application with a CIDR of 10.0.0.0/16 and VPC-Database with a CIDR of 20.0.0.0/16.

<p>
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/vpc-a-1.png" height="40%" width="48%"/>
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/vpc-b-1.png" height="40%" width="48%"/>
</p>

<p align="center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/vpc-a-2.png" height="55%" width="75%"/>
</p>

<p align="center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/vpc-b-2.png" height="55%" width="75%"/>
</p>

<h3 align="left"> Creating The Internet Gateways</h3>
Next, I created the Internet Gateways and attached each of them to the appropriate VPC.

<p>
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/application-igw.png" height="40%" width="48%"/>
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/database-igw.png" height="40%" width="48%"/>
</p>

<p align="center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/attaching-app-igw-to-vpc.png" height="55%" width="75%"/>
</p>
<h5 align="center"> Attaching Application IGW to Application VPC</h5>

<p align="center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/attaching-database-igw-to-vpc.png" height="55%" width="75%"/>
</p>
<h5 align="center"> Attaching Database IGW to Database VPC</h5>


<h3 align="left"> Creating the Subnets</h3>

Next, I created a public subnet in both VPCs and edited the subnet settings to allocate IPv4 addresses to the subnets.

<p>
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/application-server-subnet1.png" height="40%" width="48%"/>
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/database-server-subnet1.png" height="40%" width="48%"/>
</p>

<p>
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/application-server-subnet2.png" height="40%" width="48%"/>
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/database-server-subnet2.png" height="40%" width="48%"/>
</p>


<h3 align="left"> Creating the Routing Tables</h3>

Next, I created a route table in each VPC (Application RT and Database RT), edited the routes to the internet through the appropriate IGW and associated each subnet with the correct route table(Application Server Subnet to Application RT and Database Server Subnet to Database RT). To avoid wrong configurations, I took note of each of the VPC IDs and Internet Gateway IDs, so that when connecting/linking services, I linked the right ones.

<p align="center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/editing-route-for-app-rt.png" height="55%" width="75%"/>
</p>

<p align="center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/associating-app-rt-to-app-server-subnet.png" height="55%" width="75%"/>
</p>

<p align="center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/editing-route-for-db-rt.png" height="55%" width="75%"/>
</p>

<p align="center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/associating-db-rt-to-db-server-subnet.png" height="55%" width="75%"/>
</p>

<h3 align="left"> Configuring Security Groups</h3>

I configured the security groups to allow SSH and HTTP connection from any IPv4 address. After the EC2 Instances had been launched, I also allowed all traffic from the Private IP address of the other server (Application Server SG allow all traffic from the Private IP Address of the Database Server and vice versa).

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/app-server-sg.png" height="55%" width="75%"/>
</p>
<h5 align="center"> Editing the Inbound Rules for the Application Server Security Group</h5>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/db-server-sg.png" height="55%" width="75%"/>
</p>
<h5 align="center"> Editing the Inbound Rules for the Database Server Security Group</h5>


<h3 align="left"> Creating EC2 Instances in Both Subnets</h3>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/application-server1.png" height="55%" width="75%"/>
</p>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/application-server2.png" height="55%" width="75%"/>
</p>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/application-server3.png" height="55%" width="75%"/>
</p>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/application-server4.png" height="55%" width="75%"/>
</p>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/database-server1.png" height="55%" width="75%"/>
</p>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/database-server2.png" height="55%" width="75%"/>
</p>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/database-server3.png" height="75%" width="55%"/>
</p>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/database-server4.png" height="55%" width="75%"/>
</p>

Once the EC2 Instances (Application Server and Database Server) have been created and running, I created the VPC Peering Connection, accepted the peering connection on one of the VPCs, modified and edited the route on each route table and carried out some tests to ensure the setup is working when I was done configuring.


<h3 align="left"> Creating the VPC Peering Connection</h3>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/app-db-peering-connection1.png" height="55%" width="75%"/>
</p>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/app-db-peering-connection2.png" height="55%" width="75%"/>
</p>

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/app-db-peering-connection3.png" height="55%" width="75%"/>
</p>

After creating the peering connection, AWS prompted me to accept the peering connection which I can just click on the action button on the peering connection dashboard (the last screenshot) to accept the connection. This is because both VPCs are in the same region (intra-region). If I created the VPC and other resources in a different region, I would have to navigate to that region to accept the peering connection.

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/accept-peering.png" height="55%" width="75%"/>
</p>
<h5 align="center"> Accepting VPC Peering connection</h5>

Modifying The Route Tables

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/app-rt-modification.png" height="55%" width="75%"/>
</p>
<h5 align="center"> Modifying the Application Server Route Table</h5>

The above modification is carried out on the application server route table, to instruct AWS to send all requests destined for the database server VPC, through the peering connection that was created, to reach the resources in that VPC.

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/db-rt-modification.png" height="55%" width="75%"/>
</p>
<h5 align="center"> Modifying the Database Server Route Table</h5>

The above modification is carried out on the database server route table, to instruct AWS to send all requests destined for the application server VPC, through the peering connection that was created, to reach the resources in that VPC.

<h3 align="left"> Test and Validation</h3>
To validate the setup, I carried out two major tests. First I SSH into each server and tried pinging the other's private IP address. Then I copied the pem keys into each of the servers and tried using SSH to log in to the other server from one using each's Private IP Address.

<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/app-server-test.png" height="75%" width="55%"/>
</p>
<h5 align="center"> Test and Validation Carried Out on Application Server(10.0.1.101)</h5>
<h5 align="center"> Pinging The Application Server (20.0.2.46) From The Database Server (10.0.1.101), And Also Using SSH to Login To The Application Server From The Database Server</h5>


<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/db-server-test.png" height="75%" width="55%"/>
</p>
<h5 align="center"> Test and Validation Carried Out on Database Server(20.0.2.46)</h5>
<h5 align="center"> Pinging The Database Server (10.0.1.101) From The Database Server (20.0.2.46), And Also Using SSH to Login To The Database Server From The Application Server</h5>


<p align= "center">
<img src="https://github.com/Topzdomain/VPC-Peering-Connection/blob/main/screenshots/copying-pem-key-to-servers.png" height="65%" width="80%"/>
</p>
<h5 align="center"> Copying the Pem Key to Each of the Servers</h5>
