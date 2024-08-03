## Integrate Amazon API Gateway (HTTP API) with Amazon CloudFront and AWS WAF

This repository contains Terraform samples to provision an [Amazon API Gateway (HTTP API)](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html) with [Amazon CloudFront](https://aws.amazon.com/cloudfront/) and [AWS WAF](https://aws.amazon.com/waf/)

**Solution diagram**

![Solution diagram](/img/solution_overview.png)

You can follow the below pre-requisites and steps to deploy the solution in an AWS account.

**Pre-requisites**

To follow along and set up this solution, you must have the following:
* An AWS account
* A device with access to your AWS account with the following:
    * Terraform installed
    * Python 3.12 installed

**Deployment steps**

Complete the following steps to provision the solution with Terraform:

1. Install the dependencies

```bash
terraform init -input=false
```

2. Preview the resources that will be deployed in your AWS account

```bash
terraform plan \
-var "region=#your-region#" \ #region where resources will be deployed (default is us-east-1)
-var "cloudfront_domain_name=#your-cloudfront-domain-name#" \ #domain name for your CloudFront distribution (optional)
-var "cloudfront_certificate_arn=arn:aws:acm:#region#:#accountid#:certificate/#certificateid#" \ #cloudfront certificate arn (required only if cloudfront_domain_name is set)
-var "domain_name=#your-api-domain-name#" \ #domain name for your API Gateway (optional)
-var "certificate_arn=arn:aws:acm:#region#:#accountid#:certificate/#certificateid#" \ #certificate arn (required only if domain_name is set)
-var "zone_id=#zoneid#" #hosted zone id (required only if domain_name is set)
```

3. Provision resources in your AWS account

```bash
terraform apply -auto-approve \
-var "region=#your-region#" \ #region where resources will be deployed (default is us-east-1)
-var "cloudfront_domain_name=#your-cloudfront-domain-name#" \ #domain name for your CloudFront distribution (optional)
-var "cloudfront_certificate_arn=arn:aws:acm:#region#:#accountid#:certificate/#certificateid#" \ #cloudfront certificate arn (required only if cloudfront_domain_name is set)
-var "domain_name=#your-api-domain-name#" \ #domain name for your API Gateway (optional)
-var "certificate_arn=arn:aws:acm:#region#:#accountid#:certificate/#certificateid#" \ #certificate arn (required only if domain_name is set)
-var "zone_id=#zoneid#" #hosted zone id (required only if domain_name is set)
```

**Cleanup**

In order to delete the solution, run the below command:

```bash
terraform destroy -auto-approve \
-var "region=#your-region#" \ #region where resources will be deployed (default is us-east-1)
-var "cloudfront_domain_name=#your-cloudfront-domain-name#" \ #domain name for your CloudFront distribution (optional)
-var "cloudfront_certificate_arn=arn:aws:acm:#region#:#accountid#:certificate/#certificateid#" \ #cloudfront certificate arn (required only if cloudfront_domain_name is set)
-var "domain_name=#your-api-domain-name#" \ #domain name for your API Gateway (optional)
-var "certificate_arn=arn:aws:acm:#region#:#accountid#:certificate/#certificateid#" \ #certificate arn (required only if domain_name is set)
-var "zone_id=#zoneid#" #hosted zone id (required only if domain_name is set)
```

Note: The secret will not be immediately deleted after running the above command. It will be scheduled for deletion. To fully delete the secret, you can the below command:

```bash
aws secretsmanager delete-secret --secret-id waf-http-api --force-delete-without-recovery
```

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.