
# Create VPC

-Create VPC with 3 AZ and 3 subnets
VPC Name: netxbytes
# Create RDS

-Standard
-MYSQL
-Free tier
-DB name: nb-ecommerce-db

```
username: admin
password: admin123
```

-Select VPC: netxbtes-vpc
-Public Access: Yes
-Chose existing SG: default

Data base authentication: password
-Create database

# Create EC2 Instance

-Name: netxbytes_ecommerce
-Select Ubuntu AMI
-Select key pair: netxbytes

Networking
-Edit the network settings 
-Change the VPC to: Netxbytes-VPC
-Make sure the subnet is public
-Make sure it in same avaibility zone as the db
-Auto assign public IP: Enable
-Allow: SSH, HTTP, HTTPS
Note: make sure you put the database in same availability zone as your ec2 to avoild inter VPC routing charges
-User data

```bash
#!/bin/bash

sudo apt update
sudo apt upgrade -y
sudo apt install lamp-server^ -y
sudo apt install mysql-client
cd /var/www/html
sudo git clone https://github.com/Jhoode/Electronix-Website.git

```

Connect to EC2

verify apache MySQL was installed and it version version and then exit

```
sudo mysql -v
```

Change  directory to the directory of the cloned website 

```
cd /var/www/html/Electronix-Website/ecom
```

Edith the PHP connection file

```
sudo nano connection.inc.php
```

modify the connection 

```
- Database endpoint
- Database username
- Database password
- Database name (this is the name of the database you created not the db identifier)
- EC2 public IP
```

Note: username; admin
![[Pasted image 20231009204245.png]]
# Connect to Database

Note: If you don't see the DB 
-Verify if they are on Same VPC
-Verify if the DB is showing Available


![[Pasted image 20231009204820.png]]

![[Pasted image 20231009204904.png]]

-from the ec2 connect to database 
	$ msql -h database-endpoint -u username -p 
	and then enter your password
	
```
sudo mysql -h nb-ecommerce-db.cv8rrxjpeztk.us-east-1.rds.amazonaws.com -u admin -p
```

##### Create tables

```mysql
create database netxbytes_ecommerce;
```

show databases

```mysql
use ecommerce
show tables;
```

Update the tables

populate the database with ecom.sql 
cd to the ecom directory and run the following command
netxbytes_ecommerce = name of the database you created above
ecom.sql = the tables from the git repo you cloned
Exit the database

```
sudo mysql -h nb-ecommerce-db.cv8rrxjpeztk.us-east-1.rds.amazonaws.com -u admin -p ecommerce < ecom.sql

```

Change only the Document Root to point to the php index instead of the apache

```
sudo nano /etc/apache2/sites-enabled/000-default.conf
```

```bash
/var/www/html/Electronix-Website/ecom
```

Restart Apache

```bash
sudo systemctl restart apache2
```





Extras

# Create ec2 AMI

-From the EC2 instance
-click on actions
-images and templates
-create image
-Enter image name: netxbytes_ecommerce
-enter description

To locate the image
under Image from the left pane
-Click AMI Catalog
-My AMI

# Create RDS snapshot (It cost money)

-Go to rds
-select the rds database instance
-select actions
-click on take snapshot

To locate snapshot
-on the left pane of the rds page
-click on snapshot

# EC2 User Data to fetch S3 Object

first create IAM policy
create IAM role
attach the policy to the role
attach the role to the ec2 instance


# EC2 User Data

```bash
#!/bin/bash

sudo apt update
sudo apt upgrade -y
sudo apt install apache2
cd /var/www/html
sudo git clone https://github.com/Jhoode/Electronix-Website.git
```


# Create read replica 
connect EC2 2 and 3 to the read replica for external read and the ec2 one with be just for writing to the database






Note:

You will incur data transfer fees because your EC2 instance and your RDS database are in different Availability Zones. To avoid incurring these charges, they must be in the same Availability Zone.

![[Pasted image 20231019214035.png]]


NOTE:
If it showing a white screen, remote error debugging has been blocked
-add this to the index.php file to see the location of the error

```
ini_set ('display_errors', '1');
```

![[Pasted image 20231018230831.png]]

```
sudo nano /var/www/html/Electronix-Website/ecom/connection.inc.php
```


