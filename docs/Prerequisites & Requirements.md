# Prerequisites & Requirements

ZIC for AWS is a single appliance that is installed in an AWS Account, preferably in the target region, to protect machines between availability zones, regions, and accounts. Installing a single ZIC on AWS is all you need to protect the whole Account.

Ensure that you meet all of the prerequisites and requirements before starting the installation.

### Zerto User Interface Supported Browsers

The ZIC user interface requires one of these Zerto Virtual Manager Supported Browsers.

| Google Chrome | Mozilla Firefox | Microsoft Internet Expolorer | Microsoft Edge | Safari |
|-- |--|--|-- |-- |
|Zerto supports the latest 2 versions| Zerto supports the latest 2 versions| Zerto no longer supports IE 11| Zerto supports the latest 2 versions | Zerto supports the latest 2 versions | The lowest supported screen resolution is 1366x768.||

The lowest supported screen resolution is 1366x768.

### ZIC Ports and Related Services

ZIC primarily uses ports 443 and 22. 

The table below provides a detailed breakdown of all of the ports used and the services that use them. Make sure that these ports are available for use by ZIC.

| Port	| Component | Notes |
|--|--|--|
|443 | Keycloak |Login|
|443 | Keycloak |Manager page|
|http, 49153 | Keycloak |Manager page|
|443 | Keycloak (API) |Create access token|
|http, 49155 | ZIC GUI |Redirected to /main/vpgs|
|443 | Traefik (API) | |
|80 | Traefik/ZIC-GUI |Redirected to 443 and to /main/vpgs|
|443 | Traefik/ZIC-GUI |Redirected to /main/vpgs|
|443 | ZIC-GUI |Redirected to /main/vpgs|
|443 | ZIC (Swagger) | |
|443 | ZIC (Swagger) | |
|443 | ZIC (API) | Multiple endpoints for operations |
|8082 | ZIC-SUPPORT |Log collection |
|http, 49154 | ZIC |Redirected to /main/vpgs|
|22 | End User CLI |SSH and a .pem key to access the ZIC shell||

### ZIC Container Outgoing Endpoints

ZIC executes calls to AWS EC2 (Amazon Elastic Compute Cloud), DynamoDB, and STS services, using their regional endpoint host name, and their global host name for the STS service. Access to these endpoints is required in the region ZIC is deployed in and in all recovery regions in order for ZIC to function properly.

**Endpoint Examples**

- Regional EC2 service endpoint in ca-central-1 region: ec2.ca-central-1.amazonaws.com
- Regional DynamoDB service endpoint in the ca-central-1 region: dynamodb.ca-central-1.amazonaws.com
- Global STS service endpoint: sts.amazonaws.com

### Appliance Connectivity Requirements

The following ZIC for AWS Appliance connectivity requirements must be met.

-	Public internet access from ZIC to the myZerto repository. The repository is hosted at zapps-registry.zerto.com
-	Network communication between AWS regions.
-	The Instance on which the ZIC Appliance is installed must use a subnet that is accessible to DynamoDB.
  See [ZIC Ports and Related Services](#ZIC-Ports-and-Related-Services) for details.
-	The ZIC Appliance should be a m5a.2xlarge machine size.

### Minimum Required IAM Role AWS Permissions

ZIC requires IAM roles to be defined and assigned to the ZIC host. IAM roles must be assigned permissions. For the AWS account used by ZIC, Zerto requires only a subset of AWS permissions. This gives the Zerto customer more security and control over their AWS environment.

The IAM role must include this subset of required AWS permissions.

Copy and paste the following template with the required IAM role and permissions, and create a policy in JSON format.

```
{
	"Version": "2012-10-17",
	"Statement": [
	{
		"Sid": "VisualEditor0",
		"Effect": "Allow",
		"Action": [
		"ec2:CopySnapshot",
		"ec2:DeleteSnapshot",
		"ec2:CreateSnapshots",
		"ec2:ModifySnapshotAttribute",
		"ec2:DescribeInstanceTypeOfferings",
		"ec2:CreateVolume",
		"ec2:AttachVolume",
		"ec2:DetachVolume",
		"ec2:ModifyVolume",
		"ec2:DeleteVolume",
		"ec2:CreateTags",
		"ec2:RunInstances",
		"ec2:DescribeImages",
		"ec2:DescribeSnapshots",
		"ec2:DescribeRegions",
		"ec2:DescribeInstances",
		"ec2:DescribeAvailabilityZones",
		"ec2:DescribeVpcs",
		"ec2:DescribeSecurityGroups",
		"ec2:DescribeNetworkInterfaces",
		"ec2:DescribeSubnets",
		"ec2:DescribeVolumes",
		"ec2:DescribeVolumeStatus",
		"ec2:DescribeInstanceAttribute",
		"ec2:DescribeInstances",
		"ec2:DescribeTags",
		"ec2:ModifyInstanceAttribute",
		"ec2:RunInstances",
		"ec2:ModifyInstanceAttribute",
		"ec2:ModifyNetworkInterfaceAttribute",
		"ec2:StartInstances",
		"ec2:TerminateInstances",
		"ec2:CreateTags",
		"ec2:DeleteTags",
		"ec2:StopInstances",
		"dynamodb:DescribeTable",
		"dynamodb:CreateTable",
		"dynamodb:PutItem",
		"dynamodb:Scan",
		"dynamodb:GetItem",
		"dynamodb:DeleteItem",
		"dynamodb:Query",
		"dynamodb:BatchGetItem",
		"dynamodb:DeleteTable",
		"dynamodb:ListTables",
		"sts:AssumeRole",
		"iam:passRole",
		"kms:CreateGrant",
		"kms:Decrypt",
		"kms:DescribeKey",
		"kms:GenerateDataKeyWithoutPlainText"
		],
	"Resource": "*"
	}
  ]
}
```
