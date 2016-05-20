# deploy-mongodb-amazon-EC2
How to deploy a production-ready mongodb instance on Amazon EC2 from scratch

### Allocate two EBS Volumes
Create a general purpose SSD (logs) and a Provisioned IOPS SSD (data) with the required settings to run your app smoothly.

### Choose the instance type
Choose a instance type according to the needs of your APP. Warning: it's extremely advisable to use a "EBS-Optimized Supported Instance", that is at least one m4.large instance (refers to the moment the document was written).
