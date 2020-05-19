

- determine version of awscli
$ aws --version


- install awscli upgrade
$ pip install awscli --upgrade



***************************
$ aws s3 ls s3://mybucket/prefix/prefix/ --recursive | grep -E '.tif$' | awk '{print $4}' > output.txt
- grabs all .tifs in recursive dir search and writes their location to a text file, with s3://directory included in filename!!
***************************



$ aws s3 ls s3://mybucket --recursive --human-readable --summarize 
  - list all files within a bucket.
  - can copy/paste directly from terminal into text file

  -------OR--------

 $ aws s3api list-objects --bucket mybucket --prefix FLAME/ --query 'Contents[].[Key]' --output text



  -------BETTER YET, USE THIS---------

  - will print list to a .txt file locally, works for listing all files in ***SINGLE PREFIX***
 $ aws s3 ls s3://mybucket/prefix/prefix/ --output text | awk '{print $4}' > output.json



  - will print list to a .txt file locally, works for listing all files in MULTIPLE PREFIXES. just need to determine which column to display ( $2 etc )
  $ aws s3api list-objects --bucket mybucket --prefix prefix/prefix/ --query 'Contents[].[Key]' --output text | awk '{print $2}' > test.txt




$ export MapboxAccessToken=sk.eyJ1IjoiZGlnaXRhbGdyu8sb2JlIiwiYSI6ImNpamJvcDB4czAwZGJ0dGtuNTdkbWt0bGMifQ.S4hvCZDACnu5ud35qUOrkA
  - add mapbox access token to terminal for aws cli commands


- switch between profiles
 $ export AWS_PROFILE=profile-name


- add a new profile
 $ aws configure --profile my-profile-name



- running a script (.sh)

   top line:  
	#!/bin/bash
	<then commands>
	<save as .sh>

   $ chmod 755 <filename.sh>

   	-this will set perms to run the script

   $ ./script.sh



- remove a prefix/dir
$ aws s3 rm s3://mybucket/prefix/prefix//prefix-i-want-to-remove/ --recursive


- copy from local to s3
$ aws s3 cp C:\\tmp\\1.2. Reference Documents and Maps\\ s3://mybucket/prefix/prefix//20190701_ReferenceDocuments/ --recursive


- copy from s3 to s3 (prefixes)
$ aws s3 cp s3://mybucket/prefix/prefix/ s3://yourbucket/prefix/prefix/ --recursive
	------> note, must include matching target prefix, or all files from within source prefix will be dropped into target without source prefix folder
	------> note, can drop all files into single dir if you do not include the matching target prefix

		aws s3 cp s3://mybucket/data1/ s3://mybucket/geo/data1/ --recursive   <----- keeps /data1/ dir structure intact
		aws s3 cp s3://mybucket/data1/ s3://mybucket/geo/ --recursive         <----- drops all files within /data1/ dir into /geo/, no /data1/ prefix



- get account details (uses sts module of aws cli, make sure fully updated)
$ pip install awscli --upgrade 
$ aws sts get-caller-identity --profile dg-maps-api



- describe user profile
$ aws opsworks --region us-east-1 describe-user-profile



- get object ACL (permissions/ownerhip of an object)
$ aws s3api get-object-acl --bucket s3://mybucket --key prefix/prefix/prefix/AOP_AS14_Q316_V0_410_341_205_9_R1C7.tif


- grant full access to an object you are copying. requires canonical id of account you wish to give access to
$ aws cp <source bucket/object> <target bucket/object> --recursive --grants full=id=b4c82e0e4006d12d582d3ac7be5150488630a284a80836994e7cb2e7283a6773


- grant ownership to the bucket owner you are copying s3 object to:
$ aws cp <source bucket/object> <target bucket/object> --recursive --acl bucket-owner-full-control

   


- sync files from within an s3 dir locally, excluding multipe file types:
$ aws s3 sync s3://mybucket/prefix/prefix/ . --exclude "*.tif" --exclude "*.geojson"
	- this actually works through subdirs as well!
