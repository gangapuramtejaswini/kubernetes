## Login to AWS Console:

Go to the AWS Management Console and log in with your credentials.
Navigate to VPC Dashboard:

In the console, search for "VPC" and select "VPC Dashboard" from the results.
Create a VPC:

Click on "Your VPCs" in the left-hand menu.
Click the "Create VPC" button.
Enter the name of the VPC, an IPv4 CIDR block (e.g., 10.0.0.0/16), and an optional IPv6 CIDR block. Select tenancy (default or dedicated).
Click "Create VPC".
Create Subnets:

Click on "Subnets" in the left-hand menu.
Click the "Create Subnet" button.
Select the VPC you created.
Enter a name for the subnet, choose an availability zone, and specify an IPv4 CIDR block for the subnet (e.g., 10.0.1.0/24).
Repeat to create additional subnets as needed.
Create an Internet Gateway:

Click on "Internet Gateways" in the left-hand menu.
Click the "Create Internet Gateway" button.
Enter a name for the internet gateway.
Click "Create internet gateway".
Attach the internet gateway to your VPC by selecting it, clicking "Actions", and then "Attach to VPC".
Create Route Tables:

Click on "Route Tables" in the left-hand menu.
Click the "Create Route Table" button.
Enter a name for the route table and select the VPC.
Click "Create".
Select the route table, click "Actions", then "Edit routes".
Add a route with the destination 0.0.0.0/0 and target as the internet gateway you created.
Click "Save routes".
Associate the route table with your subnets by selecting "Subnet Associations", clicking "Edit subnet associations", and selecting the subnets.
Allocate and Associate an Elastic IP Address:

Go to the "Elastic IPs" section in the left-hand menu.
Click "Allocate Elastic IP address".
Click "Allocate".
Select the newly allocated Elastic IP, click "Actions", and then "Associate Elastic IP address".
Choose the instance or network interface you want to associate the Elastic IP with, and click "Associate".
