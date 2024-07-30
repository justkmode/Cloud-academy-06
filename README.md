# Cloud-academy-06
Week 5 &amp; 6 - AWS Fundamentals - 🚀 Exercise - Design a AWS VPC

Here is the updated architecture diagram and explanation that includes all the components discussed: 1 VPC, 2 Availability Zones, 6 Subnets (3 in each AZ: Public, Application, and Database), Internet Gateway, NAT Gateway, and Route Tables for Subnets.

### Updated Architecture Diagram

### VPC and Subnets

```
+--------------------------------------------------+
|                      VPC                         |
|                    10.0.0.0/16                   |
| +----------------+  +----------------+           |
| | Public Subnet  |  | Public Subnet  |           |
| | 10.0.1.0/24    |  | 10.0.2.0/24    |           |
| | (AZ 1)         |  | (AZ 2)         |           |
| |  +----------+  |  | +----------+   |           |
| |  | IGW      |  |  | | IGW      |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | NAT GW   |  |  | | NAT GW   |   |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | App Subnet    |  | App Subnet    |           |
| | 10.0.3.0/24    |  | 10.0.4.0/24    |           |
| | (AZ 1)         |  | (AZ 2)         |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | DB Subnet     |  | DB Subnet     |           |
| | 10.0.5.0/24    |  | 10.0.6.0/24    |           |
| | (AZ 1)         |  | (AZ 2)         |           |
| +----------------+  +----------------+           |
+--------------------------------------------------+

```

### Route Tables and Security

```
+--------------------------------------------------+
|                      VPC                         |
|                    10.0.0.0/16                   |
| +----------------+  +----------------+           |
| | Public Subnet  |  | Public Subnet  |           |
| | 10.0.1.0/24    |  | 10.0.2.0/24    |           |
| | (AZ 1)         |  | (AZ 2)         |           |
| |  +----------+  |  | +----------+   |           |
| |  | Pub RT   |  |  | | Pub RT   |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | SG - Web |  |  | | SG - Web |   |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | App Subnet    |  | App Subnet    |           |
| | 10.0.3.0/24    |  | 10.0.4.0/24    |           |
| | (AZ 1)         |  | (AZ 2)         |           |
| |  +----------+  |  | +----------+   |           |
| |  | Priv RT  |  |  | | Priv RT  |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | SG - App |  |  | | SG - App |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | NACL -    |  |  | | NACL -    | |           |
| |  | App/DB    |  |  | | App/DB    | |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | DB Subnet     |  | DB Subnet     |           |
| | 10.0.5.0/24    |  | 10.0.6.0/24    |           |
| | (AZ 1)         |  | (AZ 2)         |           |
| |  +----------+  |  | +----------+   |           |
| |  | Priv RT  |  |  | | Priv RT  |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | SG - DB  |  |  | | SG - DB  |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | NACL -    |  |  | | NACL -    | |           |
| |  | DB        |  |  | | DB        | |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
+--------------------------------------------------+

```

### Explanation of Elements:

1. **VPC and Subnets**:
    - The VPC is represented with the CIDR block `10.0.0.0/16`.
    - There are two Availability Zones (AZ 1 and AZ 2).
    - Each AZ contains three subnets:
        - Public Subnet (`10.0.1.0/24` in AZ 1, `10.0.2.0/24` in AZ 2).
        - Application Subnet (`10.0.3.0/24` in AZ 1, `10.0.4.0/24` in AZ 2).
        - Database Subnet (`10.0.5.0/24` in AZ 1, `10.0.6.0/24` in AZ 2).
2. **Internet Gateway (IGW) and NAT Gateway**:
    - An IGW is connected to the VPC.
    - A NAT Gateway is placed in one of the public subnets for internet access from private subnets.
3. **Route Tables**:
    - Public Route Table (`Pub RT`) includes a route to the IGW.
    - Private Route Table (`Priv RT`) includes a route to the NAT Gateway.
4. **Security Groups and NACLs**:
    - Security Groups (`SG - Web`, `SG - App`, and `SG - DB`) are associated with instances in each subnet.
    - Network Access Control Lists (`NACL - App/DB` and `NACL - DB`) for each subnet to control traffic at the subnet level.

### Tools to Use:

- [**Draw.io](http://draw.io/) ([Diagrams.net](http://diagrams.net/))**: Free and easy-to-use diagramming tool.
- **Lucidchart**: Professional diagramming tool with AWS icons.
- **Microsoft Visio**: Comprehensive diagramming tool.
- **AWS Architecture Icons**: Download from AWS to ensure accurate representation of components.

### Deliverables:

1. **Architecture Diagram**: This visual representation includes VPC, subnets, route tables, NAT Gateway, IGW, security groups, and NACLs.
2. **System Design Document**:
    - **VPC Setup**: Describe the VPC and subnets.
    - **Internet Connectivity**: Detail the use of IGW and NAT Gateway.
    - **Route Tables**: Explain route table configurations for public and private subnets.
    - **Security Measures**: Document the security groups and NACLs used to secure the VPC.
    - **High Availability**: Describe how the architecture ensures high availability (e.g., multiple subnets across different AZs).

This approach ensures a secure, highly available, and scalable architecture for Cloud Growth Limited's web application.

not fully right answers

### Secure VPC Architecture Design for Cloud Growth Limited

### Objective

To design a secure and highly available VPC architecture on AWS for a new web application with a public-facing web component and a backend database. The web component should be accessible from the Internet, while the database should only be accessible within the VPC.

### Requirements Breakdown

1. **VPC Design**:
    - CIDR block: `10.0.0.0/16`
2. **Subnet Design**:
    - Two public subnets in different Availability Zones (AZs) for high availability.
        - Public Subnet 1 (AZ1): `10.0.1.0/24`
        - Public Subnet 2 (AZ2): `10.0.2.0/24`
    - Four private subnets in different AZs for application servers and databases.
        - Private Subnet 1 (App Servers, AZ1): `10.0.3.0/24`
        - Private Subnet 2 (App Servers, AZ2): `10.0.4.0/24`
        - Private Subnet 3 (Databases, AZ1): `10.0.5.0/24`
        - Private Subnet 4 (Databases, AZ2): `10.0.6.0/24`
3. **Internet Connectivity**:
    - Internet Gateway (IGW) attached to the VPC for public subnets.
    - NAT Gateway in Public Subnet 1 for private subnet instances to access the Internet.
4. **Route Tables**:
    - Public Route Table (associated with public subnets):
        - Route for Internet traffic (`0.0.0.0/0`) pointing to IGW.
    - Private Route Table (associated with private subnets):
        - Route for Internet traffic (`0.0.0.0/0`) pointing to the NAT Gateway.
5. **Security**:
    - Security Groups (SGs) and Network Access Control Lists (NACLs) to control inbound and outbound traffic.
    - Database security: Databases in private subnets only accessible from application servers.

### Architecture Diagram

```
      +------------------------------- VPC (10.0.0.0/16) -------------------------------+
      |                                                                               |
      |  +-----------+             +-----------+             +-----------+            |
      |  | Public    |             | Private   |             | Private   |            |
      |  | Subnet 1  |             | Subnet 1  |             | Subnet 3  |            |
      |  | (10.0.1.0/24)           | (10.0.3.0/24)           | (10.0.5.0/24)          |
      |  |           |             |           |             |           |            |
      |  +-----+-----+             +-----+-----+             +-----+-----+            |
      |        |                          |                         |                 |
      |        |                          |                         |                 |
      |        |  +---------+             |   +---------+           |                 |
      |        +->|  NAT    |             +-->|  App    |           +--->| Database   |
      |           | Gateway |             |   | Servers |           |    | Servers    |
      |           +----+----+             |   +----+----+           |    +----+----+  |
      |                |                  |        |                |         |       |
      |                |                  |        |                |         |       |
      |  +-----------+ |                  +------> |                |         |       |
      |  | Public    | |                             |               |         |       |
      |  | Subnet 2  | +-----------------------------+               +---------+       |
      |  | (10.0.2.0/24)                                                           |   |
      |  |           |                                                             |   |
      |  +-----+-----+                                                             |   |
      |        |                                                                   |   |
      |        |                                                                   |   |
      |        |                                                                   |   |
      |        |          +---------+             +---------+            +---------+   |
      |        +--------->|   IGW   |             |  Private|            |  Private|   |
      |                   +----+----+             |  Subnet2|            |  Subnet4|   |
      |                        |                  |  (10.0.4|            |  (10.0.6|   |
      |                        |                  |  .0/24) |            |  .0/24) |   |
      |                        |                  +----+----+            +----+----+   |
      |                        |                                                        |
      +------------------------+--------------------------------------------------------+

```

### VPC Setup and Configuration

### 1. VPC Design

- **CIDR Block**: `10.0.0.0/16`
- **Subnets**:
    - **Public Subnet 1**: `10.0.1.0/24` in AZ1
    - **Public Subnet 2**: `10.0.2.0/24` in AZ2
    - **Private Subnet 1**: `10.0.3.0/24` in AZ1 for application servers
    - **Private Subnet 2**: `10.0.4.0/24` in AZ2 for application servers
    - **Private Subnet 3**: `10.0.5.0/24` in AZ1 for databases
    - **Private Subnet 4**: `10.0.6.0/24` in AZ2 for databases

### 2. Internet Connectivity

- **Internet Gateway (IGW)**:
    - Attach IGW to the VPC.
    - Update the public route table to route `0.0.0.0/0` traffic to the IGW.
- **NAT Gateway**:
    - Place NAT Gateway in Public Subnet 1.
    - Update the private route table to route `0.0.0.0/0` traffic to the NAT Gateway.

### 3. Route Tables

- **Public Route Table**:
    - Associate with Public Subnet 1 and Public Subnet 2.
    - Route: `0.0.0.0/0` -> IGW
- **Private Route Table**:
    - Associate with Private Subnet 1, Private Subnet 2, Private Subnet 3, and Private Subnet 4.
    - Route: `0.0.0.0/0` -> NAT Gateway

### 4. Security

- **Security Groups**:
    - **Web Servers Security Group**:
        - Inbound: Allow HTTP (port 80) and HTTPS (port 443) from anywhere.
        - Outbound: Allow all traffic.
    - **App Servers Security Group**:
        - Inbound: Allow traffic from Web Servers Security Group on the required ports (e.g., port 80 for HTTP).
        - Outbound: Allow all traffic.
    - **Database Servers Security Group**:
        - Inbound: Allow traffic from App Servers Security Group on the required database ports (e.g., port 3306 for MySQL).
        - Outbound: Allow all traffic.
- **NACLs**:
    - Apply more restrictive rules if needed, for an additional layer of security.

### Documentation

### 1. VPC Design

The VPC is designed to ensure high availability and security by distributing resources across multiple Availability Zones. Public subnets host the web servers and NAT Gateway, while private subnets host application servers and databases.

### 2. Internet Connectivity

Public subnets access the Internet through an IGW, ensuring that web servers are reachable. Private subnets use a NAT Gateway to access the Internet for updates without being exposed directly.

### 3. Route Tables

Separate route tables for public and private subnets ensure proper routing. Public subnets route Internet-bound traffic to the IGW, while private subnets route through the NAT Gateway.

### 4. Security

Security is enforced through Security Groups and NACLs. Only necessary traffic is allowed between layers (web, app, database), and direct access to databases from the Internet is prevented.

### Conclusion

This architecture ensures high availability, security, and efficient traffic management. By leveraging AWS VPC components and best practices, the design addresses the requirements for launching a secure and scalable web application on AWS.

### Assumptions

- The architecture assumes two Availability Zones for simplicity and high availability.
- Default VPC components are used unless otherwise specified.

This detailed architecture provides a robust foundation for deploying the web application while ensuring security and high availability.

To create a secure and highly available VPC architecture for Cloud Growth Limited, you need to design an architecture diagram that includes VPC components, route tables, and security configurations. Here’s a step-by-step guide on how to include these elements in your architecture diagram:

### Steps to Create the Architecture Diagram

1. **Create a Basic Layout**: Begin with the basic layout of your VPC, including all subnets and components.
2. **Add VPC and Subnets**:
    - **VPC**: Represent the VPC with a box and label it with the CIDR block (e.g., `10.0.0.0/16`).
    - **Public Subnets**: Draw two public subnets (one in each availability zone) and label them with their CIDR blocks (e.g., `10.0.1.0/24` and `10.0.2.0/24`).
    - **Private Subnets**: Draw four private subnets (two in each availability zone) and label them with their CIDR blocks (e.g., `10.0.3.0/24`, `10.0.4.0/24`, `10.0.5.0/24`, and `10.0.6.0/24`).
3. **Add Internet Gateway**: Place an Internet Gateway (IGW) and connect it to the VPC.
4. **Add NAT Gateway**: Place a NAT Gateway in one of the public subnets.
5. **Add Route Tables**:
    - **Public Route Table**: Draw a route table for the public subnets and show the route to the Internet Gateway.
    - **Private Route Table**: Draw a route table for the private subnets and show the route to the NAT Gateway.
6. **Add Security Groups and NACLs**:
    - **Security Groups**: Represent security groups associated with instances in each subnet.
    - **NACLs**: Represent Network Access Control Lists for each subnet.
7. **Add Instances and Database**:
    - **Web Servers**: Place web servers in the public subnets.
    - **Application Servers**: Place application servers in the private subnets.
    - **Database**: Place the database instances in the private subnets.

### Tools to Use

You can use diagramming tools such as Lucidchart, [Draw.io](http://draw.io/), or AWS Architecture Icons with any graphic design software.

### Detailed Diagram Elements

### VPC and Subnets

```
+--------------------------------------------------+
|                      VPC                         |
|                    10.0.0.0/16                   |
| +----------------+  +----------------+           |
| | Public Subnet  |  | Public Subnet  |           |
| | 10.0.1.0/24    |  | 10.0.2.0/24    |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.3.0/24    |  | 10.0.4.0/24    |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.5.0/24    |  | 10.0.6.0/24    |           |
| +----------------+  +----------------+           |
|                                                  |
+--------------------------------------------------+

```

### Internet Gateway and NAT Gateway

```
+--------------------------------------------------+
|                      VPC                         |
|                    10.0.0.0/16                   |
| +----------------+  +----------------+           |
| | Public Subnet  |  | Public Subnet  |           |
| | 10.0.1.0/24    |  | 10.0.2.0/24    |           |
| |  +----------+  |  |                |           |
| |  | IGW      |  |  |                |           |
| |  +----------+  |  |                |           |
| |  +----------+  |  |                |           |
| |  | NAT GW   |  |  |                |           |
| |  +----------+  |  |                |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.3.0/24    |  | 10.0.4.0/24    |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.5.0/24    |  | 10.0.6.0/24    |           |
| +----------------+  +----------------+           |
|                                                  |
+--------------------------------------------------+

```

### Route Tables

```
+--------------------------------------------------+
|                      VPC                         |
|                    10.0.0.0/16                   |
| +----------------+  +----------------+           |
| | Public Subnet  |  | Public Subnet  |           |
| | 10.0.1.0/24    |  | 10.0.2.0/24    |           |
| |  +----------+  |  |                |           |
| |  | IGW      |  |  |                |           |
| |  +----------+  |  |                |           |
| |  +----------+  |  |                |           |
| |  | NAT GW   |  |  |                |           |
| |  +----------+  |  |                |           |
| |  +----------+  |  | +----------+   |           |
| |  | Pub RT   |  |  | | Pub RT   |   |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.3.0/24    |  | 10.0.4.0/24    |           |
| |  +----------+  |  | +----------+   |           |
| |  | Priv RT  |  |  | | Priv RT  |   |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.5.0/24    |  | 10.0.6.0/24    |           |
| +----------------+  +----------------+           |
|                                                  |
+--------------------------------------------------+

```

### Security Groups and NACLs

```
+--------------------------------------------------+
|                      VPC                         |
|                    10.0.0.0/16                   |
| +----------------+  +----------------+           |
| | Public Subnet  |  | Public Subnet  |           |
| | 10.0.1.0/24    |  | 10.0.2.0/24    |           |
| |  +----------+  |  |                |           |
| |  | IGW      |  |  |                |           |
| |  +----------+  |  |                |           |
| |  +----------+  |  |                |           |
| |  | NAT GW   |  |  |                |           |
| |  +----------+  |  |                |           |
| |  +----------+  |  | +----------+   |           |
| |  | Pub RT   |  |  | | Pub RT   |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | SG - Web |  |  | | SG - Web |   |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.3.0/24    |  | 10.0.4.0/24    |           |
| |  +----------+  |  | +----------+   |           |
| |  | Priv RT  |  |  | | Priv RT  |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | SG - App |  |  | | SG - App |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | NACL -    |  |  | | NACL -    | |           |
| |  +----------+  |  | | App/DB    | |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |

```

To show 4 private subnets (2 in each Availability Zone) in the architecture diagram, you need to expand the layout to include all the private subnets. Here’s an updated version of the diagram with the additional subnets included:

### Updated Architecture Diagram

### VPC and Subnets

```
+--------------------------------------------------+
|                      VPC                         |
|                    10.0.0.0/16                   |
| +----------------+  +----------------+           |
| | Public Subnet  |  | Public Subnet  |           |
| | 10.0.1.0/24    |  | 10.0.2.0/24    |           |
| |  +----------+  |  |                |           |
| |  | IGW      |  |  |                |           |
| |  +----------+  |  |                |           |
| |  +----------+  |  |                |           |
| |  | NAT GW   |  |  |                |           |
| |  +----------+  |  |                |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.3.0/24    |  | 10.0.4.0/24    |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.5.0/24    |  | 10.0.6.0/24    |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.7.0/24    |  | 10.0.8.0/24    |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.9.0/24    |  | 10.0.10.0/24   |           |
| +----------------+  +----------------+           |
+--------------------------------------------------+

```

### Internet Gateway and NAT Gateway

```
+--------------------------------------------------+
|                      VPC                         |
|                    10.0.0.0/16                   |
| +----------------+  +----------------+           |
| | Public Subnet  |  | Public Subnet  |           |
| | 10.0.1.0/24    |  | 10.0.2.0/24    |           |
| |  +----------+  |  |                |           |
| |  | IGW      |  |  |                |           |
| |  +----------+  |  |                |           |
| |  +----------+  |  |                |           |
| |  | NAT GW   |  |  |                |           |
| |  +----------+  |  |                |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.3.0/24    |  | 10.0.4.0/24    |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.5.0/24    |  | 10.0.6.0/24    |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.7.0/24    |  | 10.0.8.0/24    |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.9.0/24    |  | 10.0.10.0/24   |           |
| +----------------+  +----------------+           |
+--------------------------------------------------+

```

### Route Tables and Security

```
+--------------------------------------------------+
|                      VPC                         |
|                    10.0.0.0/16                   |
| +----------------+  +----------------+           |
| | Public Subnet  |  | Public Subnet  |           |
| | 10.0.1.0/24    |  | 10.0.2.0/24    |           |
| |  +----------+  |  |                |           |
| |  | IGW      |  |  |                |           |
| |  +----------+  |  |                |           |
| |  +----------+  |  |                |           |
| |  | NAT GW   |  |  |                |           |
| |  +----------+  |  |                |           |
| |  +----------+  |  | +----------+   |           |
| |  | Pub RT   |  |  | | Pub RT   |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | SG - Web |  |  | | SG - Web |   |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.3.0/24    |  | 10.0.4.0/24    |           |
| |  +----------+  |  | +----------+   |           |
| |  | Priv RT  |  |  | | Priv RT  |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | SG - App |  |  | | SG - App |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | NACL -    |  |  | | NACL -    | |           |
| |  | App/DB    |  |  | | App/DB    | |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.5.0/24    |  | 10.0.6.0/24    |           |
| |  +----------+  |  | +----------+   |           |
| |  | Priv RT  |  |  | | Priv RT  |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | SG - App |  |  | | SG - App |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | NACL -    |  |  | | NACL -    | |           |
| |  | App/DB    |  |  | | App/DB    | |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.7.0/24    |  | 10.0.8.0/24    |           |
| |  +----------+  |  | +----------+   |           |
| |  | Priv RT  |  |  | | Priv RT  |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | SG - App |  |  | | SG - App |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | NACL -    |  |  | | NACL -    | |           |
| |  | App/DB    |  |  | | App/DB    | |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
| +----------------+  +----------------+           |
| | Private Subnet |  | Private Subnet |           |
| | 10.0.9.0/24    |  |

10.0.10.0/24   |           |
| |  +----------+  |  | +----------+   |           |
| |  | Priv RT  |  |  | | Priv RT  |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | SG - App |  |  | | SG - App |   |           |
| |  +----------+  |  | +----------+   |           |
| |  +----------+  |  | +----------+   |           |
| |  | NACL -    |  |  | | NACL -    | |           |
| |  | App/DB    |  |  | | App/DB    | |           |
| |  +----------+  |  | +----------+   |           |
| +----------------+  +----------------+           |
+--------------------------------------------------+

```

### Explanation of Elements:

1. **VPC and Subnets**:
    - The VPC is represented with the CIDR block `10.0.0.0/16`.
    - There are two public subnets (`10.0.1.0/24` and `10.0.2.0/24`).
    - Four private subnets (`10.0.3.0/24`, `10.0.4.0/24`, `10.0.5.0/24`, `10.0.6.0/24`, `10.0.7.0/24`, `10.0.8.0/24`, `10.0.9.0/24`, `10.0.10.0/24`).
2. **Internet Gateway (IGW) and NAT Gateway**:
    - An IGW is connected to the VPC.
    - A NAT Gateway is placed in one of the public subnets for internet access from private subnets.
3. **Route Tables**:
    - Public Route Table (`Pub RT`) includes a route to the IGW.
    - Private Route Table (`Priv RT`) includes a route to the NAT Gateway.
4. **Security Groups and NACLs**:
    - Security Groups (`SG - Web` and `SG - App`) are associated with instances in each subnet.
    - Network Access Control Lists (`NACL - App/DB`) for each subnet to control traffic at the subnet level.

### Tools to Use:

- [**Draw.io](http://draw.io/) ([Diagrams.net](http://diagrams.net/))**: Free and easy-to-use diagramming tool.
- **Lucidchart**: Professional diagramming tool with AWS icons.
- **Microsoft Visio**: Comprehensive diagramming tool.
- **AWS Architecture Icons**: Download from AWS to ensure accurate representation of components.

### Deliverables:

1. **Architecture Diagram**: This visual representation includes VPC, subnets, route tables, NAT Gateway, IGW, security groups, and NACLs.
2. **System Design Document**:
    - **VPC Setup**: Describe the VPC and subnets.
    - **Internet Connectivity**: Detail the use of IGW and NAT Gateway.
    - **Route Tables**: Explain route table configurations for public and private subnets.
    - **Security Measures**: Document the security groups and NACLs used to secure the VPC.
    - **High Availability**: Describe how the architecture ensures high availability (e.g., multiple subnets across different AZs).

This approach ensures a secure, highly available, and scalable architecture for Cloud Growth Limited's web application.
