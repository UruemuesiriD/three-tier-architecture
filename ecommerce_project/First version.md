
Create VPC 
--
with minimum of 2 availability zones
-Select VPC and More

![Pasted image 20230625123219.png](images/Pasted%20image%2020230625123219.png)

![Pasted image 20230625123320.png](images/Pasted%20image%2020230625123320.png)

![Pasted image 20230625123605.png](images/Pasted%20image%2020230625123605.png)

![Pasted image 20230625123721.png](images/Pasted%20image%2020230625123721.png)

![Pasted image 20230625123919.png](images/Pasted%20image%2020230625123919.png)

This is what the out come should look like

![Pasted image 20230625124123.png](images/Pasted%20image%2020230625124123.png)

Create EC2 instance
--

![Pasted image 20230625124310.png](images/Pasted%20image%2020230625124310.png)

![Pasted image 20230625124445.png](images/Pasted%20image%2020230625124445.png)

Create key pair

![Pasted image 20230625124814.png](images/Pasted%20image%2020230625124814.png)

![Pasted image 20230625124951.png](images/Pasted%20image%2020230625124951.png)

-Edith network settings

![Pasted image 20230625125042.png](images/Pasted%20image%2020230625125042.png)

-Select the ecom vpc
-enable auto assign public IP
-
![Pasted image 20230625125615.png](images/Pasted%20image%2020230625125615.png)

-Still under network add security group rules
HTTP & HTTPS

![Pasted image 20230625125921.png](images/Pasted%20image%2020230625125921.png)

![Pasted image 20230625130824.png](images/Pasted%20image%2020230625130824.png)

![Pasted image 20230625130900.png](images/Pasted%20image%2020230625130900.png)

![Pasted image 20230625130918.png](images/Pasted%20image%2020230625130918.png)

Connect to the EC2 Instance

![Pasted image 20230625131056.png](images/Pasted%20image%2020230625131056.png)

-Update apt cache

![Pasted image 20230625133330.png](images/Pasted%20image%2020230625133330.png)

Create MSQL RDS
--

![Pasted image 20230625133547.png](images/Pasted%20image%2020230625133547.png)

![Pasted image 20230625133807.png](images/Pasted%20image%2020230625133807.png)

![Pasted image 20230625133935.png](images/Pasted%20image%2020230625133935.png)

database:

name: ecom-database
Username; admin123
password: mypassword

![Pasted image 20230625134150.png](images/Pasted%20image%2020230625134150.png)

Select the VPC

![Pasted image 20230625205901.png](images/Pasted%20image%2020230625205901.png)

Note: Make sure the sure the ec2 instance  is on public subnet
![Pasted image 20230625205339.png](images/Pasted%20image%2020230625205339.png)

![Pasted image 20230625205526.png](images/Pasted%20image%2020230625205526.png)

To connect to subnet this is neccessary (Ignore)

![Pasted image 20230625205655.png](images/Pasted%20image%2020230625205655.png)

![Pasted image 20230625205755.png](images/Pasted%20image%2020230625205755.png)

	
Setup EC2 (DB Server )
--

update cache
install lamp server

	$ sudo apt install lamp-server^
	
![Pasted image 20230625175040.png](images/Pasted%20image%2020230625175040.png)

-Install MSQL Client

	$ sudo apt install mysql-client
	
![Pasted image 20230625175330.png](images/Pasted%20image%2020230625175330.png)

-Verified that apache is installed

	$ cd /var/www/html
	
![Pasted image 20230625175515.png](images/Pasted%20image%2020230625175515.png)

-Clone the ecom site from GitHub
		
	$ sudo git clone https://github.com/Jhoode/Electronix-Website.git

![Pasted image 20230625195802.png](images/Pasted%20image%2020230625195802.png)
	 Note: connection.inc .php is going to connect the ec2 and the rds
	 $ cd Electronix-Website/ecom/
	 
![Pasted image 20230625200428.png](images/Pasted%20image%2020230625200428.png)


- connect to the database
	
	
$ mysql -h ecom-database.cslgmy1hb3xc.us-east-2.rds.amazonaws.com -u admin123 -p

Note: if this does not connect you directly to the data base you need to go to the EC2 security group and add the mysql ports 3306 from anywhere.
	
![Pasted image 20230625200726.png](images/Pasted%20image%2020230625200726.png)

Note: if you don't see the database (ecom) just create a new

$ create database ecom
				
![Pasted image 20230625200502.png](images/Pasted%20image%2020230625200502.png)
		
$ use ecom
$ show tables;

![Pasted image 20230625202516.png](images/Pasted%20image%2020230625202516.png)
		
-Create tables 
	-copy the ecom.sql from the git repo
	![Pasted image 20230625201106.png](images/Pasted%20image%2020230625201106.png)

-Copy everything from line 30 to 353
	 ![Pasted image 20230625201217.png](images/Pasted%20image%2020230625201217.png)
-Paste in the ecom database 
		
![Pasted image 20230625201441.png](images/Pasted%20image%2020230625201441.png)
		

	$ show tables;
	
![Pasted image 20230625202711.png](images/Pasted%20image%2020230625202711.png)
-Exit the database


![Pasted image 20230625203837.png](images/Pasted%20image%2020230625203837.png)


![Pasted image 20230625203707.png](images/Pasted%20image%2020230625203707.png)

![Pasted image 20230625204436.png](images/Pasted%20image%2020230625204436.png)

Go to the Url: 

	3.145.170.165/Electronix-Website/ecom/)
	
![Pasted image 20230625204547.png](images/Pasted%20image%2020230625204547.png)


![Pasted image 20230625210743.png](images/Pasted%20image%2020230625210743.png)



Note: go into the appache to point the server to the index.apache
https://chat.openai.com/share/9283ef8e-cf0b-4dd8-b3d2-781dc8efdeb8
https://www.digitalocean.com/community/tutorials/how-to-configure-the-apache-web-server-on-an-ubuntu-or-debian-vps
https://www.codeproject.com/Questions/5312954/How-to-set-index-php-as-default-page-in-apache-lin

Error:

![Pasted image 20230625132842.png](images/Pasted%20image%2020230625132842.png)

Solution the EC2 was in a private subnet during creation
-When i changed it to public subnet i was able to connect

![IB6-Clou25-VPC-04-25_01_26_30.png](images/IB6-Clou25-VPC-04-25_01_26_30.png)


Error: Need to be on a default tenacy

![Pasted image 20230625173021.png](images/Pasted%20image%2020230625173021.png)


![Pasted image 20230625172807.png](images/Pasted%20image%2020230625172807.png)


Notes: The EC@ and the Data base should be on the same subnet else "you will not be able to connect" 

![Pasted image 20230625181124.png](images/Pasted%20image%2020230625181124.png)

	-Verified the avaibility zone

![Pasted image 20230625181341.png](images/Pasted%20image%2020230625181341.png)

![Pasted image 20230625181445.png](images/Pasted%20image%2020230625181445.png)

-you can connect to the db from the EC2 but you will be charged extra

![Pasted image 20230625181716.png](images/Pasted%20image%2020230625181716.png)

![Pasted image 20230625181824.png](images/Pasted%20image%2020230625181824.png)