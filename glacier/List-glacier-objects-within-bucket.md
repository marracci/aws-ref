#---------
# generate a list of objects that are on glacier, using a query and piping it to .txt file
# details how to list objects on s3, print to txt file.
# '{print $2}' determines the field in the output you want to print
# in this case '2' signified third field, which returns file path and file name together
# results will vary depending on storage method
# --------


# List all Glacier objects within a specific bucket
aws s3api list-objects-v2 --bucket mybucket --query "Contents[?StorageClass=='GLACIER']" --output text | awk '{print $2}' > bucket-glacier-objects.txt




# List all Glacier objects in specific prefixes within buckets
aws s3api list-objects-v2 --bucket mybucket --prefix myprefix --query "Contents[?StorageClass=='GLACIER']" --output text | awk '{print $2}' > output.txt


to script this over many prefixes:


#!/bin/bash
aws s3api list-objects-v2 --bucket mybucket --prefix myprefix1 --query "Contents[?StorageClass=='GLACIER']" --output text | awk '{print $2}' > glacier-restore_prefix1.txt
aws s3api list-objects-v2 --bucket mybucket --prefix myprefix2 --query "Contents[?StorageClass=='GLACIER']" --output text | awk '{print $2}' > glacier-restore_prefix2.txt
aws s3api list-objects-v2 --bucket mybucket --prefix myprefix3 --query "Contents[?StorageClass=='GLACIER']" --output text | awk '{print $2}' > glacier-restore_prefix3.txt
aws s3api list-objects-v2 --bucket mybucket --prefix myprefix4 --query "Contents[?StorageClass=='GLACIER']" --output text | awk '{print $2}' > glacier-restore_prefix4.txt
aws s3api list-objects-v2 --bucket mybucket --prefix myprefix5 --query "Contents[?StorageClass=='GLACIER']" --output text | awk '{print $2}' > glacier-restore_prefix5.txt

