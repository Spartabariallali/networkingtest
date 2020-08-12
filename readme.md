### Networking Fundamentals

## creating VPC (Virtual Private Cloud)

N - tier architecture

Monolithic  - One machine/server that runs all the constitutuent parts fo a business. Including: DBs, Logic and presentations
N - tier
Microservices


N - tier - division of system into logical tiers.
This is implemented through networking which allows system architects the ability to create flexibility for the application as well as security

#### VPC Virtual Private Cloud
-  virtual private cloud allows for the creation of a virtual private network that an individual can access from anywhere in the world

#### Internet gateway

#### NACLs Network Acess Control List
- network access control lists - firewall at the level of the subnet

#### Route Tables
- Set of rules that determine the flow of traffic within the VPC. It usually conducts traffic incoming from the Internet gateway

#### security Groups
- Firewall at the level of the EC2 instance

#### EC2 - Elastic computing

### Creating a VPC using AWS

steps
1. select vpc from aws services
A. ensure region is ireland

2. create vpc from vpc menu not wizard
A. tag = Eng67.NAME.P.VPC
B. Ipv4 CIDR block = 245.20.0.0/16
C. leave everything else >> create vpc

3. create internet gateway
A. click on internet gateway - create
B. tag = Eng67.NAME.P.IGW
C. attach to vpc
D. select yours, attach gateway

4. create public subnet
A. click on subnets - create subnet
B. tag = Eng67.NAME.P.Subnet.Public
C. select your vpc
D. 245.20.1.0/24 in IPv4 block
E. create

5. create private subnet
A. click on subnets - create subnet
B. tag = Eng67.NAME.P.Subnet.private
C. select your vpc
D. ip = 245.20.2.0/24, create

6.create route table
- want to build in rigidity to limit damage from lack of understanding junior member might do
- make clear connecting to internet
- want to default to private
A. check route table not assoicated with VPC already
	- keep for now
	- rename
B. Select route tables, create route table
C. Add tag =Eng67.Max.P.Route.Public
D. select your vpc
E. create vpc
F. Edit Route - add 0.0.0.0/0
	- target = internet gateway, choose your internet gateway
G. Subnet associations
	- edit subnet associations
	- add public subnet

7. Secrity group
- egress rules
	- defualt 0.0.0.0/0 auto set
	- allows everything to exit
- ingress rules (rules for entry)
- webapp needs:

- nacls for public
	- by default outbound traffic is denie
	- is stateless?
	- rule numbers matter
	- can deny IP as well as all0w
- ingress rules
	- port 22 from our IP
	- 80 for inter
	- 443
	- ephemeral on 0.0.0.0/0
	- 27017 to allow connection to private (db) subnet
- egress rules
	- allow all for now
- rules for public server
	- allow all outbound traffic to public server (245.20.1.0/24)xc
	- ingress 27017 from public server (245.20.1.0/24)
A. create new nacl
B. tag = Eng67.NAME.P.Route.NACL
C. add rule
