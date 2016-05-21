# deploy-mongodb-amazon-EC2
How to deploy a production-ready mongodb instance on Amazon EC2 from scratch

### Allocate three EBS Volumes
Create two general purpose SSD (to logs and journal) and Provisioned IOPS SSD (data) with the required settings to run your app smoothly.

### Choose the instance type
Choose the instance type according to the needs of your APP. Warning: it's extremely advisable to use a "EBS-Optimized Supported Instance", that is at least one m4.large instance (refers to the moment the document was written). Start the instance.

### Install mongodb
Create a `/etc/yum.repos.d/mongodb-org-3.0.repo` file.
```
[mongodb-org-3.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2013.03/mongodb-org/3.0/x86_64/
gpgcheck=0
enabled=1
```
Install mongodb with one command:
```
[ec2-user ~]$ sudo yum install -y mongodb-org
```
Tell MongoDB to start at boot
```
[ec2-user ~]$ sudo chkconfig mongod on
```
### Attach the EBS volume to the instance
Attach all the previously created volumes to the instance.

```
[ec2-user ~]$ sudo mkdir /data /log /journal
[ec2-user ~]$ lsblk
[ec2-user ~]$ sudo mkfs -t ext4 /data
[ec2-user ~]$ sudo mkfs -t ext4 /log
[ec2-user ~]$ sudo mkfs -t ext4 /journal
[ec2-user ~]$ sudo mount /data
[ec2-user ~]$ sudo mount /journal
[ec2-user ~]$ sudo mount /log
[ec2-user ~]$ sudo chown mongod:mongod /data /journal /log
[ec2-user ~]$ sudo ln -s /journal /data/journal
```
### Start mongodb
```
[ec2-user ~]$ sudo service mongod start
```
to test if mongodb is ok
```
[ec2-user ~]$ mongo
```
