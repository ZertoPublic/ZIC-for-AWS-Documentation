## ZIC Installation

The installation installs the following components:

- **Zerto In-Cloud Manager** </br>
  A containerized application that manages everything required for the orchestration and replication between the protected and recovery availability zones, regions, and accounts in AWS. ZIC leverages native AWS platform snapshots and manages the SLA using the Zerto journal and familiar Zerto protection components and methods.
 
  ![ZIC_ZIC_Manager1](Images/ZIC_ZIC_Manager1.png?raw=true)
  
- **Zerto In-Cloud Appliance** </br>
  A single AWS Instance Appliance that protects any account, region or availability zone to any AWS account, region, or availability zone.

- **Networking** </br>
  ZIC requires at least one VPC, Subnet and Security Group to exist in the target region.

- **Keycloak** </br>
  Keycloak is an open-source identity and access management tool, which is used for user and component authentication. It is deployed automatically as part of the ZIC installation.

- **Zerto Analytics** </br>
  A Zerto user interface which provides a view over all existing VPGs.
