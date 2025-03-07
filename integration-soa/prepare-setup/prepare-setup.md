# Prepare Setup

## Introduction
This lab will show you how to download the Oracle Resource Manager (ORM) stack zip file needed to set up the resource needed to run this workshop.

*Estimated Lab Time:* 10 minutes

### Objectives
-   Download ORM stack
-   Configure an existing Virtual Cloud Network (VCN)

### Prerequisites
This lab assumes you have:
- An Oracle Cloud account

## Task 1: Download Oracle Resource Manager (ORM) stack zip file
1.  Click on the link below to download the Resource Manager zip file you need to build your environment:

    - [appdev-int-soa-mkplc-freetier.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/vCqOmWXrgh-pg9oAXgxJNZ3xjAgqgCvNS8JQ9WQkHpDkRiBz6ll0sJsSteV3Q-LX/n/natdsecurity/b/stack/o/appdev-int-soa-mkplc-freetier.zip)

2.  Save in your downloads folder.

We strongly recommend using this stack to create a self-contained/dedicated VCN with your instance(s). Skip to *Task 3* to follow our recommendations. If you would rather use an existing VCN then proceed to the next task to update your existing VCN with the required Ingress rules.

## Task 2: Adding security rules to an existing VCN

This workshop requires a certain number of ports to be available, a requirement that can be met by using the default ORM stack execution that creates a dedicated VCN. In order to use an existing VCN/subnet, the following rules should be added to the security list.

### **(1) Ingress Rules**

|Stateless          |Source Type	|Source CIDR	|IP Protocol	|Source Port Range	|Destination Port Range	|Description                |
| :-----------      |  :--------:   |  :--------:   | :----------:  | :------------:    | :-----------------:   | :------------------------ |
|False (unchecked)  |CIDR           |0.0.0.0/0      |TCP            |All                |22                     |SSH                        |
|False (unchecked)  |CIDR           |0.0.0.0/0      |TCP            |All                |80                     |Remote Desktop using noVNC |
{: title="List of Required Network Security Rules (Ingress)"}

1.  Go to *Networking >> Virtual Cloud Networks*
2.  Choose your network
3.  Under Resources, select Security Lists
4.  Click on Default Security Lists under the Create Security List button
5.  Click *Add Ingress Rules* button
6.  Create a rule for each entry in the *Ingress* table(s) above.  
    - Stateless: Leave unchecked (Default)
    - Source Type: CIDR
    - Source CIDR: 0.0.0.0/0
    - IP Protocol: TCP
    - Source Port Range: All (Keep Default)
    - Destination Port Range: *Select from the above table(s)*
    - Description: *Select the corresponding description from the above table(s)*
7. Click *+Another Ingress Rule* and repeat step [6] until a rule is created for each port listed in the *Ingress* tables
8.  Click the Add Ingress Rules button

### **(2) Egress Rules**

|Stateless          |Source Type	|Destination CIDR	|IP Protocol	|Source Port Range	|Destination Port Range	|Description                |
| :-----------      |  :--------:   |  :--------:       | :----------:  | :------------:    | :-----------------:   | :------------------------ |
|False (unchecked)  |CIDR           |0.0.0.0/0          |TCP            |All                |80                     |Outbound HTTP access       |
|False (unchecked)  |CIDR           |0.0.0.0/0          |TCP            |All                |443                    |Outbound HTTPS access      |
{: title="List of Required Network Security Rules (Egress)"}

1.  Select *Egress Rule* from the left panel
2.  Click Add Egress Rule button
3.  Create a rule for each entry in the *Egress* table(s) above:  
    - Stateless: Leave unchecked (Default)
    - Source Type: CIDR
    - Destination CIDR: 0.0.0.0/0
    - IP Protocol: TCP
    - Source Port Range: All (Keep Default)
    - Destination Port Range: *Select from the above table(s)*
    - Description: *Select the corresponding description from the above table(s)*
4. Click *+Another Egress Rule* and repeat step [3] until a rule is created for each port listed in the *Egress* tables
5.  Click the Add Egress Rules button

## Task 3: Setup Compute   
Using the details from the two Tasks above, proceed to the lab *Environment Setup* to set up your workshop environment using Oracle Resource Manager (ORM) and one of the following options:
-  Create Stack:  *Compute + Networking*
-  Create Stack:  *Compute only* with an existing VCN where security lists have been updated as per *Task 2* above

You may now proceed to the next lab.

## Acknowledgements
* **Author** - Rene Fontcha, LiveLabs Platform Lead, NA Technology
* **Contributors** - Meghana Banka
* **Last Updated By/Date** - Rene Fontcha, LiveLabs Platform Lead, NA Technology, February 2023
