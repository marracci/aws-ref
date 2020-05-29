AWS RDS - backing up mySQL database manually

# relies on creating a snapshot of the dbase, using awscli
# your IAM user must have RDS policies enabled.
# determine what db instances you have available:


aws rds describe-db-instances


# When you create a DB snapshot using the AWS CLI, you need to identify which DB instance you are going to back up, and then give your DB snapshot a name so you can restore from it later. You can do this by using the AWS CLI create-db-snapshot command:
#

$ aws rds create-db-snapshot --db-instance-identifier mydbinstancename --db-snapshot-identifier mydbsnapshotname 


-----------------------------------------------------------
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateSnapshot.html