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
  <img src="https://img.shields.io/badge/terraform-v0.14-green" alt="Terraform">
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


We eat, drink, sleep and most importantly love **DevOps**. We are working towards strategies for standardizing architecture while ensuring security for the infrastructure. We are strong believer of the philosophy <b>Bigger problems are always solved by breaking them into smaller manageable problems</b>. Resonating with microservices architecture, it is considered best-practice to run database, cluster, storage in smaller <b>connected yet manageable pieces</b> within the infrastructure.

This module is basically combination of [Terraform open source](https://www.terraform.io/) and includes automatation tests and examples. It also helps to create and improve your infrastructure with minimalistic code instead of maintaining the whole infrastructure code yourself.

We have [*fifty plus terraform modules*][terraform_modules]. A few of them are comepleted and are available for open source usage while a few others are in progress.




## Prerequisites

This module has a few dependencies:

- [Terraform 0.13](https://learn.hashicorp.com/terraform/getting-started/install.html)
- [Go](https://golang.org/doc/install)
- [github.com/stretchr/testify/assert](https://github.com/stretchr/testify)
- [github.com/gruntwork-io/terratest/modules/terraform](https://github.com/gruntwork-io/terratest)







## Examples


**IMPORTANT:** Since the `master` branch used in `source` varies based on new modifications, we suggest that you use the release versions [here](https://github.com/clouddrove/terraform-aws-cloudtrail/releases).


### Simple Example
Here is an example of how you can use this module in your inventory structure:
```hcl
    module "cloudtrail" {
      source                        = "clouddrove/cloudtrail/aws"
      version                       = "0.13.0"

      name                          = "cloudtrail"
      repository                    = "https://registry.terraform.io/modules/clouddrove/cloudtrail/aws/latest"
      environment                   = "security"
      label_order                   = ["name", "environment"]
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
|------|-------------|------|---------|:--------:|
| attributes | Additional attributes (e.g. `1`). | `list(string)` | `[]` | no |
| cloud\_watch\_logs\_group\_arn | Specifies a log group name using an Amazon Resource Name (ARN), that represents the log group to which CloudTrail logs will be delivered. | `string` | `""` | no |
| cloud\_watch\_logs\_role\_arn | Specifies the role for the CloudWatch Logs endpoint to assume to write to a user’s log group. | `string` | `""` | no |
| data\_resource | Specify if you want your event selector to include management events for your trail. | `bool` | `true` | no |
| data\_resource\_type | The resource type in which you want to log data events. You can specify only the following value: `AWS::S3::Object` `AWS::Lambda::Function`. | `string` | `"AWS::S3::Object"` | no |
| data\_resource\_values | Specifies an event selector for enabling data event logging, It needs to be a list of map values. See: https://www.terraform.io/docs/providers/aws/r/cloudtrail.html for details on this map variable. | `list(string)` | `[]` | no |
| enable\_log\_file\_validation | Specifies whether log file integrity validation is enabled. Creates signed digest for validated contents of logs. | `bool` | `true` | no |
| enable\_logging | Enable logging for the trail. | `bool` | `true` | no |
| enabled\_cloudtrail | If true, deploy the resources for the module. | `bool` | `true` | no |
| environment | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `""` | no |
| event\_selector | Specifies an event selector for enabling data event logging. Fields documented below. Please note the CloudTrail limits when configuring these. | `bool` | `true` | no |
| event\_selector\_data\_resource | Specifies logging data events. Fields documented below. | `bool` | `false` | no |
| include\_global\_service\_events | Specifies whether the trail is publishing events from global services such as IAM to the log files. | `bool` | `true` | no |
| include\_management\_events | Specify if you want your event selector to include management events for your trail. | `bool` | `true` | no |
| is\_organization\_trail | The trail is an AWS Organizations trail. | `bool` | `false` | no |
| kms\_key\_id | Specifies the KMS key ARN to use to encrypt the logs delivered by CloudTrail. | `string` | `""` | no |
| label\_order | Label order, e.g. `name`,`application`. | `list(any)` | `[]` | no |
| managedby | ManagedBy, eg 'CloudDrove'. | `string` | `"hello@clouddrove.com"` | no |
| name | Name  (e.g. `app` or `cluster`). | `string` | n/a | yes |
| read\_write\_type | Specify if you want your trail to log read-only events, write-only events, or all. By default, the value is All. | `string` | `"All"` | no |
| repository | Terraform current module repo | `string` | `""` | no |
| s3\_bucket\_name | S3 bucket name for CloudTrail log. | `string` | n/a | yes |
| sns\_topic\_name | Specifies the name of the Amazon SNS topic defined for notification of log file delivery. | `string` | `null` | no |
| tags | Additional tags (e.g. map(`BusinessUnit`,`XYZ`). | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | The Amazon Resource Name of the trail. |
| home\_region | The region in which the trail was created. |
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
