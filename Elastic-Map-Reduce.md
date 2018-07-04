---
layout: page
---

# Elastic Map Reduce

## Wat is EMR
EMR stands for Elastic MapReduce. We use EMR to run Hadoop jobs on large datasets. EMR spins up a cluster of Amazon instances that executes the job, then terminates. It is a cheap way to work with big data.

## Setting up EMR Command Line Interface
**If you can do the steps below, you can also try it from the browser. The nice part about CLI is you can do interactive jobs more easily which means you don't have to set up local [Hadoop](Hadoop) to test**

It is actually pretty simple to set up. Follow [instructions here](http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-cli-install.html). The following tips are meant to *supplement* the instructions so follow the amazon instructions and go here if you get stuck.

1.  The EMR CLI requires Ruby 1.8.7. This is an old version (current is above 2.0). For easy installation and management of these different versions, you can use Ruby Version Manager. See http://rvm.io/rvm/install
   ```curl -sSL https://get.rvm.io | bash -s stable```
   installs RVM. The following line must also be in your .bashrc to activate rvm
   ```source ~/.rvm/scripts/rvm```
   To install / use ruby 1.8.7 run
   ```rvm install 1.8.7-p374 && rvm use 1.8.7-p374@emr-cli --create```
   Then
   ```ruby -v```
   should be 1.8.7-p374

2.  You must fill in ```credentials.json``` for requires several fields.
  * access_id / private_key are in a credentials.csv file. Either you or Patrick have it. Ask if you can't find it.
  * key-pair / key-pair-file: create a key-pair file via http://docs.aws.amazon.com/IAM/latest/UserGuide/ManagingUserCerts.html (note: you probably already have openssl if you have linux). You must '''give the pem file to Patrick''' so we can associate it with your user account.
  * Use "log_uri": "s3://gt-big-data-club/logs",
  * Use "region": "us-east-1"

A good way to test out if EMR will work for you is to do this tutorial with [Google NGrams](https://aws.amazon.com/articles/5249664154115844)
