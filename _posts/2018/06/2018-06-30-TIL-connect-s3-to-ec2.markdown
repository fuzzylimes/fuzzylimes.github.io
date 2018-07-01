---
layout: post
title:  "TIL: Connecting an S3 bucket to EC2 instance"
date:   2018-06-30 20:30:00 -0000
categories: TIL
---
So one of the things that came up yesterday afternoon while working with getting the symbolic links and public folder setup was storing my files off on an s3 instances instead of trying to store it all on the image. I'd had the thought about it before, but never really had the time to sit down and dive into what all that involves. So today I spent a bit of time researching what all has to be done to get up and running with S3 bucket in an EC2 instance.

## Creating an S3 Bucket
So before you can start, you'll actually need to create an S3 bucket. To do so, [amazon has this guide](https://docs.aws.amazon.com/quickstarts/latest/s3backup/step-1-create-bucket.html) that breaks down the steps to get you up and running... but there's also [another page here](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/create-bucket.html) that also outlines the process. At least the second one gives more info about how to set it up so that it's not public...

But these pages didn't really answer all of my questions, like [what about the pricing?](https://aws.amazon.com/s3/pricing/) Or what about locking down content so that people can't get to it?

## Create IAM Role for S3 Access
In order to handle the permission access over to the S3 instance, we need to create a new IAM Role and User that will be allowed to access the instance.

To do so, we first start by creating a new IAM Role through the IAM dashboard. The IAM Role will be set to `AmazonS3FullAccess`. This will give full read and write access to any IAM user within this group.

## Assign the IAM Role to Instance
When starting up a brand new EC2 instance, you have the option (on step 3) to assign an IAM role at configuration time. You'd set this to be the role created in the previous section.

If you already have an exiting EC2 instance that's running, you can simple go and edit the `Instance Settings` for that EC2 instance and attach a new IAM role to it. [This guide here](https://aws.amazon.com/blogs/security/easily-replace-or-attach-an-iam-role-to-an-existing-ec2-instance-by-using-the-ec2-console/) outlines that entire process for you.

## Use the aws cli to access bucket
Assuming that you've deployed with amazon linux (if you haven't, you're going to have to [install awscli](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) to start using the commands), you're ready to start accessing your data!

Running the `aws s3 ls` should return back a list of the buckets that are available to your account.

From this point, [read the aws cli](https://docs.aws.amazon.com/cli/latest/reference/s3/) documentation on how you can access items in your bucket. [This page](https://docs.aws.amazon.com/cli/latest/userguide/using-s3-commands.html) has a little bit more info that makes it more clear of how to actually access that data.

💚