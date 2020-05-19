s3express basic commands

***Create Profile***
saveauth ACCESSKEY SECRETACCESSKEY [name]

***Load a previously saved profile***
loadauth [name]

***Show all saved profiles***
showauth <all>

***Remove saved profile***
rmauth [name]



**OPTIONS**

setopt -retry:10 -retrywait:5
setopt -reset

showopt


pwd = show local working directory

-purge = delete files that are no longer present in source location



***list subdirectories only***
ls bucket -od
ls bucket/subdir -od 

***list all objects in all subdirs***
ls bucket -s

***list objects and subdirs***
ls bucket -s -d

***show size in bytes***
ls bucket/subdir -bytes

***show summary of total objects***
ls bucket -s -sum



**PUT**

*put c:\folder\ bucket/subdir -onlydiff*
upload files in c:\folder\to mybucket only if they are different compared to the matching file that is already on S3. Different files are files that have the same path and the same name but a different MD5 value. Files that have already a corresponding file with matching MD5, will not be uploaded

*put c:\folder\ bucket/subdir -onlynewer*
Only upload files that are newer compared to the matching files that are already on S3. 
Newer files are files that have the same path and the same name but a newer modified time. 
Newer files are also files that are not yet uploaded to S3. 
So using the '-onlynewer' flag uploads files that are not yet on S3 plus all the files whose timestamp is newer compared to files already on S3.


**DELETE**

***delete all objects within location that have same extension***
del bucket/subdir/*.txt 									  ***

***delete all objects within bucket***
del bucket/* -s

***simulation objects which would be deleted***
del bucket/* -sim


