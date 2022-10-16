+++
title = "About"
description = "About Eugene"
date = "2022-10-14"
aliases = ["about-us", "contact"]
author = "Eugene"
+++

## Who I am

Hi! I'm an engineer who loves working with computers. I like to untangle and solve complex or unusual problems, be it a software bug or a highly-architectured infrastructure in the public cloud.

Apart from work, I like heading out to nature, hiking, biking and bread making. I make very nice sourdough bread.

## Tech

My *nix journey started some time in very early 2000s, when my friend came to me with a stack of DVDs containing FreeBSD 3.6
and said: "and now we're going to compile the kernel for your computer".

I lived in the FreeBSD console for a few years (did you know you could watch movies in full console mode?!) and then slowly transitioned to Gentoo Linux for better hardware support.

Many years later, after using MacOS for a while, I'm now on Arch. Btw.

During those years, I picked up some programming languages, and what started as just shell scripting with glue like awk, sed and wc grew into learning Python and later Go.
I can read and make small fixes in many other languages too, but can't say I'm good at them. Well, I can't say that about neither of Python nor Go :)

However, I like to write tools that solve some problems, such as:

1. https://github.com/springload/ssm-parent - basically, allows you to store your configuration in SSM Parameter store, and then read it recursively at once, combine it together and present as env vars to your Dockerfile entrypoint.
2. https://github.com/springload/aws-ssh - it's all about ssh-ing into AWS EC2. Imagine you have more than 50 different AWS accounts with ec2 instances that can go up and down all the time. In addition to that, your coworker has just started and wants to SSH into one of those old instances. This tool solves that problem: firstly it gathers info about all running ec2 instances, and then utilises ec2 connect feature of AWS to push a temporary ssh key into the instance.
3. https://github.com/springload/ecs-tool - just allows to deploy to AWS ECS with ease either locally or in the CI/CD pipeline.

I like to contribute to Open Source whenever I can, but I feel I need to dedicate more time to it. I've made some minor contributions into tools I used and found some issues, notably these were:

1. terraform aws provider
2. terragrunt
3. pulumi
4. gocloud.dev

I've worked with pretty much all public clouds, and I hold the AWS DevOps Professional certificate.
