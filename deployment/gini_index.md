# [Gini Index](http://gini-index.genee.cn)
It is the main repository for Gini modules.

## Check/Set Current Gini Version
```
$ gini version
my-module/1.2.0

$ gini version 1.3.0-beta
my-module/1.3.0-beta
```
## Publish/Unpublish Modules
Publish/Unpublish process use `git-archive` to prepare package. So you have to correctly tag specified commit.
```
$ cd /path/to/my-module
$ git tag 1.2.0
```
### Do It in Regular Way
```
$ gini index publish 1.2.0
User: doejohn
Password:
my-module/1.2.0 was published successfully.

$ gini index unpublish 1.2.0
User: doejohn
Password:
my-module/1.2.0 was unpublished successfully.
```
### Do It without Password Promption
```
$ gini index login doejohn
Password:
You've successfully logged in as doejohn!

$ gini index who
Hey! You are doejohn.

$ gini index publish 1.2.0
my-module/1.2.0 was published successfully.

$ gini index unpublish 1.2.0
my-module/1.2.0 was unpublished successfully.

$ gini index logout
You are logged out now.

$ gini index who
Oops. You are NOBODY.
```

## Install a Gini Module
```
$ gini install my-module '*'
Fetching INDEX file for my-module...
Downloading my-module from my-module/1.2.0.tgz...
Extracting my-module to /path/to/my-module...
```
