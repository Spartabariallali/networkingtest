### Networking Fundamentals

# What is networking?

A computer network comprises two or more computers that are connected—either by cables (wired) or WiFi (wireless)—with the purpose of transmitting, exchanging, or sharing data and resources. You build a computer network using hardware (e.g., routers, switches, access points, and cables) and software (e.g., operating systems or business applications).

Geographic location often defines a computer network. For example, a LAN (local area network) connects computers in a defined physical space, like an office building, whereas a WAN (wide area network) can connect computers across continents. The internet is the largest example of a WAN, connecting billions of computers worldwide.

You can further define a computer network by the protocols it uses to communicate, the physical arrangement of its components, how it controls traffic, and its purpose.

Computer networks enable communication for every business, entertainment, and research purpose. The internet, online search, email, audio and video sharing, online commerce, live-streaming, and social
networks all exist because of computer networks.

- **Nodes**: A node is a connection point inside a network that can receive, send, create, or store data. Each node requires you to provide some form of identification to receive access,
like an IP address. A few examples of nodes include computers, printers, modems, bridges, and switches. A node is essentially any network device that can recognize, process, and transmit information to any other network node.
- **Routers**: A router is a physical or virtual device that sends information contained in data packets between networks. Routers analyze data within the packets to determine the best way for the information to reach its ultimate destination. Routers forward data packets until they reach their destination node.
- **Switches**: A switch is a device that connects other devices and manages node-to-node communication within a network, ensuring data packets reach their ultimate destination. While a router
sends information between networks, a switch sends information between nodes in a single network. When discussing computer networks,
‘switching’ refers to how data is transferred between devices in a network. The three main types of switching are as follows:
    - *Circuit switching*, which establishes a dedicated communication path between nodes in a network. This dedicated path assures the full bandwidth is available during the transmission, meaning no other traffic can travel along that path.
    - *Packet switching* involves breaking down data into independent components called packets which, because of their small size, make fewer demands on the network. The packets travel through the
    network to their end destination.
    - *Message switching* sends a message in its entirety from the source node, traveling from switch to switch until it reaches its destination node.
- **Ports**: A port identifies a specific connection between network devices. Each port is identified by a number. If you think of an IP address as comparable to the address of a hotel, then
ports are the suites or room numbers within that hotel. Computers use numbers to determine which application, service, or process should
receive specific messages.
- **Network cable types**: The most common network cable types are Ethernet twisted pair, coaxial, and fiber optic. The choice of cable type depends on the size of the network, the arrangement of
network elements, and the physical distance between devices.

### Subnet masks

A single IP address identifies both a network, and a unique interface on that network. A subnet mask can also be written in dotted decimal notation and determines where the network part of an IP address ends, and the host portion of the address begins.

When expressed in binary, any bit set to one means the corresponding bit in the IP address is part of the network address. All the bits set to zero mark the corresponding bits in the IP address as part of the host
address.

The bits marking the subnet mask must be consecutive ones. Most subnet masks start with 255. and continue on until the network mask ends. A Class C subnet mask would be 255.255.255.0.

# IPv4 vs IPv6

- IPv4 is 32-Bit IP address whereas IPv6 is a 128-Bit IP address.
- IPv4 is a numeric addressing method whereas IPv6 is an alphanumeric addressing method.
- IPv4 binary bits are separated by a dot(.) whereas IPv6 binary bits are separated by a colon(:).
- IPv4 offers 12 header fields whereas IPv6 offers 8 header fields.
- IPv4 supports broadcast whereas IPv6 doesn’t support broadcast.
- IPv4 has checksum fields while IPv6 doesn’t have checksum fields
- IPv4 supports VLSM (Virtual Length Subnet Mask) whereas IPv6 doesn’t support VLSM.
- IPv4 uses ARP (Address Resolution Protocol) to map to MAC address whereas IPv6 uses NDP (Neighbour Discovery Protocol) to map to MAC address.

## Features of IPv4

- Connectionless Protocol
- Allow creating a simple virtual communication layer over diversified devices
- It requires less memory, and ease of remembering addresses
- Already supported protocol by millions of devices
- Offers video libraries and conferences

## Features of IPv6

- Hierarchical addressing and routing infrastructure
- Stateful and Stateless configuration
- Support for quality of service (QoS)
- An ideal protocol for neighboring node interaction

## Computer network types

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
C. Add tag =Eng67.NAME.P.Route.Public
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
