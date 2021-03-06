# Some Terraform Examples

In this repository I'm keeping a few terraform examples that I made during my first attempts to learn the tool. My initial goal was to be able to spin up an environment with outbound internet connectivity that I could use for testing an anytime, and explore some of the features of terraform.

## Requirements

terraform version 0.12 syntax is used, so please make sure you're at <= terraform 0.12

## Invocation

Both templates take two variables, the REGION and PROFILE

```
terraform plan -out liam.plan -var="region=us-east-2" -var="profile=saml"
```

Region should be the AWS region you want to deploy to, formatted the official manner, EG: "us-east-1" or "us-west-2". Should work fine withe very region. Defaults to us-east-1.

profile should be the profile within .aws/credentials that terraform will use to execute. Normally this is default, but if you've done a little customization you can override the default. Defaults to "default"

Due note that it is necesarry to include variables in terraform destroy later as well.

## vpc_with_nat_gw.tf

This will create a two subnet-vpc with a nat GW, and the public/private routing setup.

It will also create a iam role/instance profile for use with SSM, so you can use SSM-Session Manager to connect into it, which is easy if you're lazy.

## vpc_with_nat_instance.tf

This will create a two subnet-vpc with a nat instance, and the public/private routing setup.

It will also create a iam role/instance profile for use with SSM, so you can use SSM-Session Manager to connect into it, which is easy if you're lazy.

Nat instances can be way cheaper than Nat gateways, and as this instance is t2.micro, it is both free tier eligible and much cheaper than a nat gateway
