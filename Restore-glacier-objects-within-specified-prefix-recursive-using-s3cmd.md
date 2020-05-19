#!/bin/bash

# restores all objects within a specified s3 prefix
# requires s3cmd to be installed locally 
# requires AWS ARN user to have s3:RestoreObject and s3:GetObject enabled on bucket policy
# will pause for several minutes, depending on how many objects are in the specified prefix; then will list all restore object cmds

set -o verbose


s3cmd restore --recursive s3://mybucket/prefix1/ --restore-days=15 --restore-priority=bulk
s3cmd restore --recursive s3://mybucket/prefix2/ --restore-days=15 --restore-priority=bulk 
s3cmd restore --recursive s3://mybucket/prefix3/ --restore-days=15 --restore-priority=bulk 
s3cmd restore --recursive s3://mybucket/prefix4/ --restore-days=15 --restore-priority=bulk 
s3cmd restore --recursive s3://mybucket/prefix5/ --restore-days=15 --restore-priority=bulk 
