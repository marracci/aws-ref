#!/bin/bash

# restores individual objects from glacier to s3 for 14 days, bulk tier pricing
# requires awscli 
# not currently working on Linux 16 with awscli 1.11.x
# use this after Glacier restore, because glacier restore in awscli is only by OBJECT...
# syncing restored objects by prefix will not work - prefixes are not restored 

aws s3api restore-object --bucket mybucket --key myprefix/mysubprefix/object1.tif --restore-request Days=14,GlacierJobParameters={Tier="Bulk"}
aws s3api restore-object --bucket mybucket --key myprefix/mysubprefix/object2.tif --restore-request Days=14,GlacierJobParameters={Tier="Bulk"}
aws s3api restore-object --bucket mybucket --key myprefix/mysubprefix/object3.tif --restore-request Days=14,GlacierJobParameters={Tier="Bulk"}
aws s3api restore-object --bucket mybucket --key myprefix/mysubprefix/object4.tif --restore-request Days=14,GlacierJobParameters={Tier="Bulk"}
aws s3api restore-object --bucket mybucket --key myprefix/mysubprefix/object5.tif --restore-request Days=14,GlacierJobParameters={Tier="Bulk"}