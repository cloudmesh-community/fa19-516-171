# Abstract Streaming interfaces for the NIST Big data Architecture/Now Changed to Cloudmesh Storage execution of AwsS3 to Local and Local to AwsS3.

Jagadeesh Kandimalla, fa19-516-171 

The streaming service initial architecure is when a Object gets added to S3 ,An AWS Lambda function will get triggered and will call the Google cloud endpoint which inturn will call the APP engine where we write the data to Google cloud Storage


# Objective

The streaming service initial architecure is when a Object gets added to S3 and S3 event will trigger AWS Lambda function and the lambda will call the Google cloud endpoint which inturn will call the APP engine where we write the data to Google cloud Storage.This way the streaming is automated ,anytime a object gets detected in S3 it is loaded to Google Storage and all the components are loosely coupled so that anytime we can replace the destination like Google Big query by just switching the app name in Google App Engine.


# Technologies

AWS S3,<br/>
AWS Lambda,<br/>
OpenAPI 3.0.2,<br/>
GCP Cloudendpoint,<br/>
GCP App Engine,<br/>
GCP Coud Storage

# Architecture

![architecture](images/architecuture-171.png)

# Progress
1.) Created a AWS account/S3 bucket - Done.  
2.) Updated the .cloudmesh.yaml file with awss3 key pair - Done   .  
3.) Debugged the Cloudmesh-Storage awss3.provdier.py and StorageABC.py and got the put and list commands working for AWS S3- Done .    
4.) Uploded the files to S3 files using Cloudmesh commands(PUT and LIST) -- Done .     
5.) Created the GCP account and set up gsutil on the mac - Done .  
6.) Created the project and bucket and created the google application credentials - Done   
7.) Download the Google app credentials and set the authentication in the environment variables - Done .   
8.) Developed a flask application to read the data and load the data to google cloud storage -Done       
9.) Debugged the flask application in the local using POSTMAN - Done .   
10.) Extend the flask application to read from the URL and get the data downloaded from URL and load in to Google cloud storage - In Progress.<br/>
11.) Development of AWS Lambda application - Not Started . 

# Project Scope changed from streaming to AwsS3 to Local and Local to AwsS3

Professor wants to fix the AwsS3 Provider and add some new functionality and test and benchmark the new chages.
Now AwsS3 provider has been fixed and and the new functionality(checking bucket exists ,if not create code) has been implemented in the provider.
Pytests have been updated to print out benchamarks and the code has been tested using Pytests and CMD commands.
All the code has been checked to Cloudmesh-Storage transfer bucket and has been merged with master.
Pytest have been changes again to remove the hardcording for storage and process them as variables.

The documentation of cloud storage has been updated and ordered properly and checked into cloudmesh-manual storage.md file

https://github.com/cloudmesh/cloudmesh-manual/blob/master/docs-source/source/storage/storage.md

# Pytest Benchmark Tests

============================= test session starts ==============================
platform darwin -- Python 3.7.4, pytest-5.2.2, py-1.8.0, pluggy-0.13.0 -- /Users/jagadeeshk/ENV3/bin/python3
cachedir: .pytest_cache
rootdir: /Users/jagadeeshk/cm/cloudmesh-storage, inifile: pytest.ini
collecting ... [34m
# ----------------------------------------------------------------------
# variables.dict()
# ----------------------------------------------------------------------
# 26:<module> ./tests/test_storage.py
# ----------------------------------------------------------------------
# {'cloud': 'AWS',
#  'cluster': 'clustera',
#  'debug': 'True',
#  'experiment': 'base',
#  'group': 'cloudmesh',
#  'key': 'jkandima',
#  'storag': 'awss3',
#  'storage': 'aws',
#  'timer': 'False',
#  'trace': 'True',
#  'verbose': '10',
#  'vm': 'Jagadeesh-vm-3'}
# ----------------------------------------------------------------------
[0m
Test run for aws
provider: <cloudmesh.storage.Provider.Provider object at 0x103646550> awss3
collected 10 items

tests/test_storage.py::TestStorage::test_create_local_source 
[35m
# ######################################################################
# test_create_local_source /tests/test_storage.py 53
# ######################################################################
[0m

TESTDIR: /Users/jagadeeshk/.cloudmesh/storage/test/a

TESTDIR: /Users/jagadeeshk/.cloudmesh/storage/test/a/b

TESTDIR: /Users/jagadeeshk/.cloudmesh/storage/test/a/b/c
PASSED
tests/test_storage.py::TestStorage::test_put 
[35m
# ######################################################################
# test_put /tests/test_storage.py 66
# ######################################################################
[0m
{'action': 'put',
 'destination': '/',
 'recursive': False,
 'source': '~/.cloudmesh/storage/test/'}
{'action': 'put',
 'destination': '/',
 'message': 'Source uploaded',
 'objlist': [{'contentLength': '12',
              'fileName': 'a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:27 GMT'},
             {'contentLength': '12',
              'fileName': 'a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:28 GMT'},
             {'contentLength': '12',
              'fileName': 'b.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:29 GMT'},
             {'contentLength': '12',
              'fileName': 'c.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:30 GMT'}],
 'recursive': False,
 'source': '~/.cloudmesh/storage/test/'}
[{'cm': {'cloud': 'aws',
         'collection': 'aws-storage',
         'created': '2019-11-15 20:51:58.533927',
         'kind': 'storage',
         'modified': '2019-11-30 16:34:30.138569',
         'name': 'a.txt'},
  'contentLength': '12',
  'fileName': 'a.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:27 GMT'},
 {'cm': {'cloud': 'aws',
         'collection': 'aws-storage',
         'created': '2019-11-15 20:51:58.533927',
         'kind': 'storage',
         'modified': '2019-11-30 16:34:30.140676',
         'name': 'a.txt'},
  'contentLength': '12',
  'fileName': 'a.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:28 GMT'},
 {'cm': {'cloud': 'aws',
         'collection': 'aws-storage',
         'created': '2019-11-15 23:38:42.063054',
         'kind': 'storage',
         'modified': '2019-11-30 16:34:30.141680',
         'name': 'b.txt'},
  'contentLength': '12',
  'fileName': 'b.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:29 GMT'},
 {'cm': {'cloud': 'aws',
         'collection': 'aws-storage',
         'created': '2019-11-15 23:38:42.067487',
         'kind': 'storage',
         'modified': '2019-11-30 16:34:30.142714',
         'name': 'c.txt'},
  'contentLength': '12',
  'fileName': 'c.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:30 GMT'}]
PASSED
tests/test_storage.py::TestStorage::test_put_recursive 
[35m
# ######################################################################
# test_put_recursive /tests/test_storage.py 88
# ######################################################################
[0m
{'action': 'put',
 'destination': '/',
 'message': 'Source uploaded',
 'objlist': [{'cm': {'cloud': 'aws',
                     'collection': 'aws-storage',
                     'created': '2019-11-15 20:51:58.533927',
                     'kind': 'storage',
                     'modified': '2019-11-30 16:34:30.138569',
                     'name': 'a.txt'},
              'contentLength': '12',
              'fileName': 'a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:27 GMT'},
             {'cm': {'cloud': 'aws',
                     'collection': 'aws-storage',
                     'created': '2019-11-15 20:51:58.533927',
                     'kind': 'storage',
                     'modified': '2019-11-30 16:34:30.140676',
                     'name': 'a.txt'},
              'contentLength': '12',
              'fileName': 'a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:28 GMT'},
             {'cm': {'cloud': 'aws',
                     'collection': 'aws-storage',
                     'created': '2019-11-15 23:38:42.063054',
                     'kind': 'storage',
                     'modified': '2019-11-30 16:34:30.141680',
                     'name': 'b.txt'},
              'contentLength': '12',
              'fileName': 'b.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:29 GMT'},
             {'cm': {'cloud': 'aws',
                     'collection': 'aws-storage',
                     'created': '2019-11-15 23:38:42.067487',
                     'kind': 'storage',
                     'modified': '2019-11-30 16:34:30.142714',
                     'name': 'c.txt'},
              'contentLength': '12',
              'fileName': 'c.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:30 GMT'}],
 'recursive': True,
 'source': '~/.cloudmesh/storage/test/'}
{'action': 'put',
 'destination': '/',
 'message': 'Source uploaded',
 'objlist': [{'contentLength': '12',
              'fileName': 'a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:31 GMT'},
             {'contentLength': '12',
              'fileName': 'a/a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:32 GMT'},
             {'contentLength': '12',
              'fileName': 'a/b/b.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:33 GMT'},
             {'contentLength': '12',
              'fileName': 'a/b/c/c.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:34 GMT'}],
 'recursive': True,
 'source': '~/.cloudmesh/storage/test/'}
[{'cm': {'cloud': 'aws',
         'collection': 'aws-storage',
         'created': '2019-11-15 20:51:58.533927',
         'kind': 'storage',
         'modified': '2019-11-30 16:34:33.984488',
         'name': 'a.txt'},
  'contentLength': '12',
  'fileName': 'a.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:31 GMT'},
 {'cm': {'cloud': 'aws',
         'collection': 'aws-storage',
         'created': '2019-11-15 23:36:23.585862',
         'kind': 'storage',
         'modified': '2019-11-30 16:34:33.985934',
         'name': 'a/a.txt'},
  'contentLength': '12',
  'fileName': 'a/a.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:32 GMT'},
 {'cm': {'cloud': 'aws',
         'collection': 'aws-storage',
         'created': '2019-11-15 23:36:23.587020',
         'kind': 'storage',
         'modified': '2019-11-30 16:34:33.987162',
         'name': 'a/b/b.txt'},
  'contentLength': '12',
  'fileName': 'a/b/b.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:33 GMT'},
 {'cm': {'cloud': 'aws',
         'collection': 'aws-storage',
         'created': '2019-11-15 23:36:23.588015',
         'kind': 'storage',
         'modified': '2019-11-30 16:34:33.988082',
         'name': 'a/b/c/c.txt'},
  'contentLength': '12',
  'fileName': 'a/b/c/c.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:34 GMT'}]
PASSED
tests/test_storage.py::TestStorage::test_get 
[35m
# ######################################################################
# test_get /tests/test_storage.py 110
# ######################################################################
[0m
{'action': 'get',
 'destination': '~/.cloudmesh/storage/test',
 'message': 'Source downloaded',
 'objlist': [{'contentLength': '12',
              'fileName': 'a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:31 GMT'}],
 'recursive': False,
 'source': '/a.txt'}
[{'cm': {'cloud': 'aws',
         'collection': 'aws-storage',
         'created': '2019-11-15 20:51:58.533927',
         'kind': 'storage',
         'modified': '2019-11-30 16:34:36.881267',
         'name': 'a.txt'},
  'contentLength': '12',
  'fileName': 'a.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:31 GMT'}]
PASSED
tests/test_storage.py::TestStorage::test_list 
[35m
# ######################################################################
# test_list /tests/test_storage.py 121
# ######################################################################
[0m
[s3.ObjectSummary(bucket_name='cloudmeshtest', key='a.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='a/a.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='a/b/b.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='a/b/c/c.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='b.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='c.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='marker.txt')]
''
'a.txt'
'a/a.txt'
'a/b/b.txt'
'a/b/c/c.txt'
'b.txt'
'c.txt'
'marker.txt'
{'action': 'list',
 'destination': '~/.cloudmesh/storage/test',
 'message': 'Source downloaded',
 'objlist': [{'contentLength': '12',
              'fileName': 'a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:31 GMT'},
             {'contentLength': '12',
              'fileName': 'b.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:29 GMT'},
             {'contentLength': '12',
              'fileName': 'c.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:30 GMT'},
             {'contentLength': '0',
              'fileName': 'marker.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 13:05:33 GMT'}],
 'recursive': False,
 'source': '/'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-15 20:51:58.533927',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:38.771511',
        'name': 'a.txt'},
 'contentLength': '12',
 'fileName': 'a.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 16:34:31 GMT'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-15 23:38:42.063054',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:38.773836',
        'name': 'b.txt'},
 'contentLength': '12',
 'fileName': 'b.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 16:34:29 GMT'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-15 23:38:42.067487',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:38.775134',
        'name': 'c.txt'},
 'contentLength': '12',
 'fileName': 'c.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 16:34:30 GMT'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-29 04:26:29.145488',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:38.776316',
        'name': 'marker.txt'},
 'contentLength': '0',
 'fileName': 'marker.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 13:05:33 GMT'}
PASSED
tests/test_storage.py::TestStorage::test_list_dir_only 
[35m
# ######################################################################
# test_list_dir_only /tests/test_storage.py 132
# ######################################################################
[0m
[s3.ObjectSummary(bucket_name='cloudmeshtest', key='a.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='a/a.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='a/b/b.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='a/b/c/c.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='b.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='c.txt'),
 s3.ObjectSummary(bucket_name='cloudmeshtest', key='marker.txt')]
''
{'action': 'list',
 'destination': '~/.cloudmesh/storage/test',
 'message': 'Source downloaded',
 'objlist': [{'contentLength': '12',
              'fileName': 'a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:31 GMT'},
             {'contentLength': '12',
              'fileName': 'a/a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:32 GMT'},
             {'contentLength': '12',
              'fileName': 'a/b/b.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:33 GMT'},
             {'contentLength': '12',
              'fileName': 'a/b/c/c.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:34 GMT'},
             {'contentLength': '12',
              'fileName': 'b.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:29 GMT'},
             {'contentLength': '12',
              'fileName': 'c.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:30 GMT'},
             {'contentLength': '0',
              'fileName': 'marker.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 13:05:33 GMT'}],
 'recursive': True,
 'source': '/'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-15 20:51:58.533927',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:41.109323',
        'name': 'a.txt'},
 'contentLength': '12',
 'fileName': 'a.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 16:34:31 GMT'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-15 23:36:23.585862',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:41.111638',
        'name': 'a/a.txt'},
 'contentLength': '12',
 'fileName': 'a/a.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 16:34:32 GMT'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-15 23:36:23.587020',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:41.113066',
        'name': 'a/b/b.txt'},
 'contentLength': '12',
 'fileName': 'a/b/b.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 16:34:33 GMT'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-15 23:36:23.588015',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:41.114198',
        'name': 'a/b/c/c.txt'},
 'contentLength': '12',
 'fileName': 'a/b/c/c.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 16:34:34 GMT'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-15 23:38:42.063054',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:41.115256',
        'name': 'b.txt'},
 'contentLength': '12',
 'fileName': 'b.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 16:34:29 GMT'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-15 23:38:42.067487',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:41.116323',
        'name': 'c.txt'},
 'contentLength': '12',
 'fileName': 'c.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 16:34:30 GMT'}
{'cm': {'cloud': 'aws',
        'collection': 'aws-storage',
        'created': '2019-11-29 04:26:29.145488',
        'kind': 'storage',
        'modified': '2019-11-30 16:34:41.117359',
        'name': 'marker.txt'},
 'contentLength': '0',
 'fileName': 'marker.txt',
 'lastModificationDate': 'Sat, 30 Nov 2019 13:05:33 GMT'}
PASSED
tests/test_storage.py::TestStorage::test_search 
[35m
# ######################################################################
# test_search /tests/test_storage.py 144
# ######################################################################
[0m
{'action': 'list',
 'destination': '~/.cloudmesh/storage/test',
 'directory': '/',
 'filename': 'a.txt',
 'message': 'File found',
 'objlist': [{'contentLength': '12',
              'fileName': 'a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:31 GMT'},
             {'contentLength': '12',
              'fileName': 'a/a.txt',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:32 GMT'}],
 'recursive': True,
 'search': 'search',
 'source': '/'}
[{'cm': {'cloud': 'aws', 'kind': 'storage', 'name': 'a.txt'},
  'contentLength': '12',
  'fileName': 'a.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:31 GMT'},
 {'cm': {'cloud': 'aws', 'kind': 'storage', 'name': 'a/a.txt'},
  'contentLength': '12',
  'fileName': 'a/a.txt',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:32 GMT'}]
PASSED
tests/test_storage.py::TestStorage::test_create_dir 
[35m
# ######################################################################
# test_create_dir /tests/test_storage.py 155
# ######################################################################
[0m
{'action': 'create_dir',
 'destination': '~/.cloudmesh/storage/test',
 'directory': 'created_dir',
 'filename': 'a.txt',
 'message': 'Directory created',
 'objlist': [{'contentLength': '0',
              'fileName': 'created_dir/',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:43 GMT'}],
 'recursive': True,
 'search': 'search',
 'source': '/'}
[{'cm': {'cloud': 'aws',
         'collection': 'aws-storage',
         'created': '2019-11-15 20:56:59.467607',
         'kind': 'storage',
         'modified': '2019-11-30 16:34:43.189342',
         'name': 'created_dir/'},
  'contentLength': '0',
  'fileName': 'created_dir/',
  'lastModificationDate': 'Sat, 30 Nov 2019 16:34:43 GMT'}]
PASSED
tests/test_storage.py::TestStorage::test_delete 
[35m
# ######################################################################
# test_delete /tests/test_storage.py 166
# ######################################################################
[0m
{'action': 'delete',
 'destination': '~/.cloudmesh/storage/test',
 'directory': 'created_dir',
 'filename': 'a.txt',
 'message': 'Source Deleted',
 'objlist': [{'contentLength': '0',
              'fileName': 'created_dir/',
              'lastModificationDate': 'Sat, 30 Nov 2019 16:34:43 GMT'}],
 'recursive': True,
 'search': 'search',
 'source': '/created_dir'}
PASSED
tests/test_storage.py::TestStorage::test_benchmark 
+----------------------+-------+---------------------+-----+-----------------------------------+------------+--------+-------------+-------------+
| timer                | time  | start               | tag | node                              | user       | system | mac_version | win_version |
+----------------------+-------+---------------------+-----+-----------------------------------+------------+--------+-------------+-------------+
| create source        | 0.001 | 2019-11-30 16:34:25 | aws | ('jagadeeshs-MacBook-Pro.local',) | jagadeeshk | Darwin | 10.14.6     |             |
| put                  | 3.84  | 2019-11-30 16:34:30 | aws | ('jagadeeshs-MacBook-Pro.local',) | jagadeeshk | Darwin | 10.14.6     |             |
| get                  | 2.89  | 2019-11-30 16:34:33 | aws | ('jagadeeshs-MacBook-Pro.local',) | jagadeeshk | Darwin | 10.14.6     |             |
| list                 | 2.337 | 2019-11-30 16:34:38 | aws | ('jagadeeshs-MacBook-Pro.local',) | jagadeeshk | Darwin | 10.14.6     |             |
| search               | 0.868 | 2019-11-30 16:34:41 | aws | ('jagadeeshs-MacBook-Pro.local',) | jagadeeshk | Darwin | 10.14.6     |             |
| create dir           | 1.197 | 2019-11-30 16:34:41 | aws | ('jagadeeshs-MacBook-Pro.local',) | jagadeeshk | Darwin | 10.14.6     |             |
| delete               | 1.232 | 2019-11-30 16:34:43 | aws | ('jagadeeshs-MacBook-Pro.local',) | jagadeeshk | Darwin | 10.14.6     |             |
| benchmark_start_stop | 0.0   | 2019-11-30 16:34:44 | aws | ('jagadeeshs-MacBook-Pro.local',) | jagadeeshk | Darwin | 10.14.6     |             |
+----------------------+-------+---------------------+-----+-----------------------------------+------------+--------+-------------+-------------+

csv,timer,time,starttag,node,user,system,mac_version,win_version
#csv,create source,0.001,None,('jagadeeshs-MacBook-Pro.local',),jagadeeshk,Darwin,10.14.6,
#csv,put,3.84,None,('jagadeeshs-MacBook-Pro.local',),jagadeeshk,Darwin,10.14.6,
#csv,get,2.89,None,('jagadeeshs-MacBook-Pro.local',),jagadeeshk,Darwin,10.14.6,
#csv,list,2.337,None,('jagadeeshs-MacBook-Pro.local',),jagadeeshk,Darwin,10.14.6,
#csv,search,0.868,None,('jagadeeshs-MacBook-Pro.local',),jagadeeshk,Darwin,10.14.6,
#csv,create dir,1.197,None,('jagadeeshs-MacBook-Pro.local',),jagadeeshk,Darwin,10.14.6,
#csv,delete,1.232,None,('jagadeeshs-MacBook-Pro.local',),jagadeeshk,Darwin,10.14.6,
#csv,benchmark_start_stop,0.0,None,('jagadeeshs-MacBook-Pro.local',),jagadeeshk,Darwin,10.14.6,

PASSED

============================= 10 passed in 20.23s ==============================




