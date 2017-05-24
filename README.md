# aws-waf-regional-security-automations

The [AWS WAF Security Automations](https://aws.amazon.com/answers/security/aws-waf-security-automations/) is a simple AWS-provided solution that helps you provision the AWS WAF Security Automations stack without worrying about creating and configuring the underlying AWS infrastructure. WARNING: This template creates AWS Lambda functions, an AWS WAFRegional Web ACL, an Amazon S3 bucket, and an Amazon CloudWatch custom metric. You will be billed for the AWS resources used if you create a stack from this template.

## Changes in this fork

The awslabs official WAF security automations repo (https://github.com/awslabs/aws-waf-security-automations) is geared towards WAF Global (Cloudfront) but I needed WAF-regional automations to be able to attach this service to an application load balancer. This is reflected in the changes. This repo has been forked from master with Pull Request 6 (longer Cloudformation stack names) rolled in.

** Note **

The stack calls an official AWS bucket in the region that you deploy to (in my case solutions-eu-west-1) and then uses the zipped functions for Lambda. Obviously this isn't going to work for WAF Regional, so you need to zip each function and upload it to a bucket of your choice (this is currently set to solutions-generic-$awsRegion within the cloudformation template). Once AWS add like-for-like functions for WAF Regional, this problem goes away.
Apologies for bundling the entire SDK into the reputation-lists-parser function, you 'may' get away with removing this when you clone the repo, uploading without it, and letting Lambda do this for you (basically function goes from 600kb to 4mb with that rolled in. Yuck.)

Source code for the AWS solution "WAS WAF(Regional) Security Automations".

## Cloudformation templates

- cform/aws-waf-security-automations.template

## log-parser

- code/log-parser/log-parser.py

## reputation-lists-parser

- code/reputation-lists-parser/reputation-lists-parser.js

## access-handler

- code/access-handler/access-handler.py

## custom-resource

- code/custom-resource/custom-resource.py

***

Copyright 2016 Amazon.com, Inc. or its affiliates. All Rights Reserved.

Licensed under the Amazon Software License (the "License"). You may not use this file except in compliance with the License. A copy of the License is located at

    http://aws.amazon.com/asl/

or in the "license" file accompanying this file. This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, express or implied. See the License for the specific language governing permissions and limitations under the License.
