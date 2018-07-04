---
layout: page
title: AWS Info
---

# AWS Info

[Log in with your credentials for GT Big Data here](https://gtbigdata.signin.aws.amazon.com/console). If you don't have them, ask^^

## Using EMR with MRJob

First, install MRJob:
`pip install mrjob`

Then, [create a key pair that will let you spin up ec2 instances](http://docs.aws.amazon.com/gettingstarted/latest/wah/getting-started-create-key-pair.html)

Next, create a config file for MRJob. Save it as `~/.mrjob.conf`
```conf
runners:
  emr:
    aws_access_key_id: <<YOUR ACCESS KEY>>
    aws_secret_access_key: <<YOUR SECRET KEY>>
    aws_region: us-east-1
    ec2_key_pair: <<The name of the EC2 keypair you created in the previous step (keypair)>>
    ec2_key_pair_file: <<The absolute path + filename of the keypair on your local machine (/home/you/keypair.pem)>>
    ec2_instance_type: m1.medium
    num_ec2_instances: 10

    s3_log_uri: s3://gt-big-data-club/logs
    s3_scratch_uri: s3://gt-big-data-club/tmp/

    # Less important
    base_tmp_dir: /tmp
    cmdenv:
      TZ: America/Chicago

  local:
    base_tmp_dir: /tmp
```

Then, to run the job in EMR with input and output from s3, you can do this:

```bash
python <my MR Job. py> -r emr s3://gt-big-data-club/<path/to/myInputFile.txt> --output-dir=s3://gt-big-data-club/<my-output-dir> --no-output
```

The official library for using MRJob is [here](http://mrjob.readthedocs.org/en/latest/)

## Uploading Data to Amazon S3
### Web UI
The easiest way to upload data is from the S3 console.

### Command line: S3CMD
We can use [s3cmd](http://s3tools.org/s3cmd) to use s3 from the command line.

First install with `sudo apt-get install s3cmd` , or follow directions on their site.

Then, run `s3cmd --configure` and input your AWS access keys.

Here's some sample interaction
#### Showing all buckets
```bash
patrick@pv--hpm6:~$ s3cmd ls
2014-01-25 19:36  s3://gt-big-data
2014-02-12 18:15  s3://gt-big-data-club
```
#### List a specific bucket
```bash
patrick@pv--hpm6:~$ s3cmd ls s3://gt-big-data-club/
                       DIR   s3://gt-big-data-club/logs/
                       DIR   s3://gt-big-data-club/movie-lens-dir/
                       DIR   s3://gt-big-data-club/tmp/
                       DIR   s3://gt-big-data-club/twitter-superbowl/
```

#### Upload a file to a bucket
*Note: The / at the end of your bucket name is important!* Without the slash, it will upload to the parent bucket of what you intended with the filename of the bucket you intended.
```bash
patrick@pv--hpm6:~/proj/twitter-superbowl/analysis$ s3cmd put top-ngrams.json s3://gt-big-data-club/twitter-superbowl/
WARNING: Module python-magic is not available. Guessing MIME types based on file extensions.
top-ngrams.json -> s3://gt-big-data-club/twitter-superbowl/top-ngrams.json  [1 of 1]
 8302786 of 8302786   100% in    0s     9.55 MB/s  done
```

#### Download a file from a bucket
 ```bash
patrick@pv--hpm6:~/proj/twitter-superbowl/analysis$ s3cmd get s3://gt-big-data-club/twitter-superbowl/top-ngrams.json top-ngrams-from-s3.json
s3://gt-big-data-club/twitter-superbowl/top-ngrams.json -> top-ngrams-from-s3.json  [1 of 1]
 8302786 of 8302786   100% in    1s     5.16 MB/s  done
```

#### Download from a bucket recursively
You can use this to download the output from a large MRJob
```bash
patrick@pv--hpm6:~/proj/MovieLens/mrjob$ s3cmd get --recursive s3://gt-big-data-club/movie-lens-dir/out
s3://gt-big-data-club/movie-lens-dir/out/_SUCCESS -> ./out/_SUCCESS  [1 of 16]
 0 of 0     0% in    0s     0.00 B/s  done
s3://gt-big-data-club/movie-lens-dir/out/part-00000 -> ./out/part-00000  [2 of 16]
 25021 of 25021   100% in    0s   106.80 kB/s  done
...
s3://gt-big-data-club/movie-lens-dir/out/part-00014 -> ./out/part-00014  [16 of 16]
 25882 of 25882   100% in    0s   133.07 kB/s  done
```


## Using EMR Command Line Interface

EMR stands for Elastic MapReduce. We use EMR to run Hadoop jobs on large datasets.

It is actually pretty simple. Follow instructions here: [http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-cli-install.html]

1.  The EMR CLI requires Ruby 1.8.7. This is an old version (current is 2.1). For easy installation and management of these different versions, you can use Ruby Version Manager. See http://rvm.io/rvm/install
  * To install RVM, run this in your terminal:
  ```bash
  $ curl -sSL https://get.rvm.io | bash -s stable
  ```
  * Afterwards, add the following line to your ``.bashrc`` or ``.zshrc`` to activate rvm
  ```bash
  source ~/.rvm/scripts/rvm
  ```
  * Open a new terminal and type in ``rvm`` to make sure everything is working correctly.
  * To install/ use ruby 1.8.7 run
  ```bash
  $ rvm install 1.8.7-p374
  $ rvm use 1.8.7-p374@emr-cli --create
  ```
  * Then if you type `ruby -v` you should get `1.8.7-p374`
2. You must fill in `credentials.json` for requires several fields.
  * access_id/ private_key are in a credentials.csv file. Either you or Patrick have it. Ask if you can't find it.
  * key-pair/ key-pair-file: create a key-pair file via http://docs.aws.amazon.com/IAM/latest/UserGuide/ManagingUserCerts.html (note: you probably already have openssl if you have Linux). You **must** give the pem file to Patrick so we can associate it with your user account.
  * Use "log_uri": "s3://gt-big-data-club/logs",
  * Use "region": "us-east-1"

A good way to test out if EMR will work for you is to do this tutorial with Google NGrams: https://aws.amazon.com/articles/5249664154115844
