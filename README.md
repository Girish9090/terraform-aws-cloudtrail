<!-- This file was automatically generated by the `geine`. Make all changes to `README.yaml` and run `make readme` to rebuild this file. -->

<p align="center"> <img src="https://user-images.githubusercontent.com/50652676/62349836-882fef80-b51e-11e9-99e3-7b974309c7e3.png" width="100" height="100"></p>


<h1 align="center">
    Terraform AWS Cloudtrail
</h1>

<p align="center" style="font-size: 1.2rem;">
    Terraform module to provision an AWS CloudTrail with encrypted S3 bucket. This bucket is used to store CloudTrail logs.
     </p>

<p align="center">

<a href="https://www.terraform.io">
  <img src="https://img.shields.io/badge/Terraform-v0.12-green" alt="Terraform">
</a>
<a href="LICENSE.md">
  <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="Licence">
</a>


</p>
<p align="center">

<a href='https://facebook.com/sharer/sharer.php?u=https://github.com/clouddrove/terraform-aws-cloudtrail'>
  <img title="Share on Facebook" src="https://user-images.githubusercontent.com/50652676/62817743-4f64cb80-bb59-11e9-90c7-b057252ded50.png" />
</a>
<a href='https://www.linkedin.com/shareArticle?mini=true&title=Terraform+AWS+Cloudtrail&url=https://github.com/clouddrove/terraform-aws-cloudtrail'>
  <img title="Share on LinkedIn" src="https://user-images.githubusercontent.com/50652676/62817742-4e339e80-bb59-11e9-87b9-a1f68cae1049.png" />
</a>
<a href='https://twitter.com/intent/tweet/?text=Terraform+AWS+Cloudtrail&url=https://github.com/clouddrove/terraform-aws-cloudtrail'>
  <img title="Share on Twitter" src="https://user-images.githubusercontent.com/50652676/62817740-4c69db00-bb59-11e9-8a79-3580fbbf6d5c.png" />
</a>

</p>
<hr>


We eat, drink, sleep and most importantly love **DevOps**. We are working towards stratergies for standardizing architecture while ensuring security for the infrastructure. We are strong believer of the philosophy <b>Bigger problems are always solved by breaking them into smaller manageable problems</b>. Resonating with microservices architecture, it is considered best-practice to run database, cluster, storage in smaller <b>connected yet manageable pieces</b> within the infrastructure.

This module is basically combination of [Terraform open source](https://www.terraform.io/) and includes automatation tests and examples. It also helps to create and improve your infrastructure with minimalistic code instead of maintaining the whole infrastructure code yourself.

We have [*fifty plus terraform modules*][terraform_modules]. A few of them are comepleted and are available for open source usage while a few others are in progress.




## Prerequisites

This module has a few dependencies:

- [Terraform 0.12](https://learn.hashicorp.com/terraform/getting-started/install.html)
- [Go](https://golang.org/doc/install)
- [github.com/stretchr/testify/assert](https://github.com/stretchr/testify)
- [github.com/gruntwork-io/terratest/modules/terraform](https://github.com/gruntwork-io/terratest)






## Examples

**IMPORTANT:** Since the `master` branch used in `source` varies based on new modifications, we suggest that you use the release versions [here](https://github.com/clouddrove/terraform-aws-cloudtrail/releases).


### Simple Example
Here is an example of how you can use this module in your inventory structure:
```hcl
    module "cloudtrail" {
      source                        = "git::https://github.com/clouddrove/terraform-aws-cloudtrail.git?ref=tags/0.12.1"
      name                          = "cloudtrail"
      application                   = "clouddrove"
      environment                   = "security"
      label_order                   = ["environment", "name", "application"]
      s3_bucket_name                = "s3-logs"
      enable_logging                = true
      enable_log_file_validation    = true
      include_global_service_events = true
      is_multi_region_trail         = false
      kms_key_id                    = "arn:aws:kms:eu-west-1:xxxxxxxxx:key/xxxxxx-xxxx-xxxx-xxxxx"
    }
```



## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| application | Application (e.g. `cd` or `clouddrove`). | string | `` | no |
| attributes | Additional attributes (e.g. `1`). | list(string) | `<list>` | no |
| cloud_watch_logs_group_arn | Specifies a log group name using an Amazon Resource Name (ARN), that represents the log group to which CloudTrail logs will be delivered. | string | `` | no |
| cloud_watch_logs_role_arn | Specifies the role for the CloudWatch Logs endpoint to assume to write to a user’s log group. | string | `` | no |
| enable_log_file_validation | Specifies whether log file integrity validation is enabled. Creates signed digest for validated contents of logs. | bool | `true` | no |
| enable_logging | Enable logging for the trail. | bool | `true` | no |
| enabled_cloudtrail | If true, deploy the resources for the module. | bool | `true` | no |
| environment | Environment (e.g. `prod`, `dev`, `staging`). | string | `` | no |
| event_selector | Specifies an event selector for enabling data event logging, It needs to be a list of map values. See: https://www.terraform.io/docs/providers/aws/r/cloudtrail.html for details on this map variable. | list(string) | `<list>` | no |
| include_global_service_events | Specifies whether the trail is publishing events from global services such as IAM to the log files. | bool | `false` | no |
| is_multi_region_trail | Specifies whether the trail is created in the current region or in all regions. | bool | `false` | no |
| is_organization_trail | The trail is an AWS Organizations trail. | bool | `false` | no |
| kms_key_id | Specifies the KMS key ARN to use to encrypt the logs delivered by CloudTrail. | string | `` | no |
| label_order | Label order, e.g. `name`,`application`. | list | `<list>` | no |
| name | Name  (e.g. `app` or `cluster`). | string | - | yes |
| s3_bucket_name | S3 bucket name for CloudTrail log. | string | - | yes |
| tags | Additional tags (e.g. map(`BusinessUnit`,`XYZ`). | map(string) | `<map>` | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | The Amazon Resource Name of the trail. |
| home_region | The region in which the trail was created. |
| id | The name of the trail. |
| tags | A mapping of tags to assign to the resource. |



## Testing

In this module testing is performed with [terratest](https://github.com/gruntwork-io/terratest) and it creates a small piece of infrastructure, matches the output like ARN, ID and Tags name etc and destroy infrastructure in your AWS account. This testing is written in GO, so you need a [GO environment](https://golang.org/doc/install) in your system.

You need to run the following command in the testing folder:
```hcl
  go test -run Test
```



## Feedback
If you come accross a bug or have any feedback, please log it in our [issue tracker](https://github.com/clouddrove/terraform-aws-cloudtrail/issues), or feel free to drop us an email at [hello@clouddrove.com](mailto:hello@clouddrove.com).

If you have found it worth your time, go ahead and give us a ★ on [our GitHub](https://github.com/clouddrove/terraform-aws-cloudtrail)!

## About us

At [CloudDrove][website], we offer expert guidance, implementation support and services to help organisations accelerate their journey to the cloud. Our services include docker and container orchestration, cloud migration and adoption, infrastructure automation, application modernisation and remediation, and performance engineering.

<p align="center">We are <b> The Cloud Experts!</b></p>
<hr />
<p align="center">We ❤️  <a href="https://github.com/clouddrove">Open Source</a> and you can check out <a href="https://github.com/clouddrove">our other modules</a> to get help with your new Cloud ideas.</p>

  [website]: https://clouddrove.com
  [github]: https://github.com/clouddrove
  [linkedin]: https://cpco.io/linkedin
  [twitter]: https://twitter.com/clouddrove/
  [email]: https://clouddrove.com/contact-us.html
  [terraform_modules]: https://github.com/clouddrove?utf8=%E2%9C%93&q=terraform-&type=&language=