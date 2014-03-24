This is for users to test their EMR credentials and get started with MRJob, EMR, and S3.
This is code from [the wiki](https://github.com/gt-big-data/wiki/wiki/AWS-Info#using-emr-with-mrjob) :)

## Starting
install mrjob with `pip install mrjob`

## Run locally
`python word_count.py sherlock-holmes.txt`

Should give a lot of job info, and then finally
```
    "chars"	549698
    "lines"	12649
    "words"	104493
```

## Run In The Cloud
Things you need from us
  1. AWS access key + AWS secret access key. We distribute these in a CSV file for your account.
  2. A password to access your account

Things you need to do:
  1. [Create an EC2 key pair](http://docs.aws.amazon.com/gettingstarted/latest/wah/getting-started-create-key-pair.html), and download it to your machine. Make sure to run `chmod 400 *myKeyPair.pem*`
    1. NOTE that you should see pdv.pem in this folder when creating your key pair. If you don't then this is not guaranteed to work.
  2. Fill in the `.mrjob.conf` file with your access key, secret access token, key pair name, and key pair path.

  A fake example of what this might look like in your `.mrjob.conf` with user bob who created the key-pair bob.pem and stored it in his configs folder

```
    aws_access_key_id: AJVLKDFAHVKNMLDFSFAJ
    aws_secret_access_key: JVMAKLA+++/fdakjlIEQLjvAL
    ec2_key_pair: bob
    ec2_key_pair_file: /home/bob/configs/bob.pem 
```

   3. Put this `.mrjob.conf` file **in your home directory**. `mv .mrjob.conf ~/`
   4. Run the job:   
```
python word_count.py -r emr s3://gt-big-data-club/mrjob-test-wordcount/sherlock-holmes.txt --output-dir=s3://gt-big-data-club/mrjob-test-wordcount/out --no-output
```
This will spin up an instance to run your job, and word count a copy of sherlock holmes we uploaded to s3 previously.
