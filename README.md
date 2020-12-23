# eq-author-terraform-dynamodb

Terraform project that creates the DocumentDB infrastructure for EQ Author

To import this module add the following code into you Terraform project:

```
module "author-documentdb" {
  source                          = "./aws-documentdb"
  env                             = "${var.env}"
  aws_account_id                  = "${var.aws_account_id}"
  aws_assume_role_arn             = "${var.aws_assume_role_arn}"
  vpc_id                          = "${module.author-vpc.vpc_id}"
  documentdb_security_group_name  = "${var.env}-author-documentdb-security-group"
  documentdb_cluster_name         = "author-documentdb"
  documentdb_subnet_group_name    = "${module.author-vpc.database_subnet_group_name}"
  application_cidrs               = "${var.author_application_cidrs}"
  master_username                 = "${var.author_mongo_username}"
  master_password                 = "${var.author_mongo_password}"
}
```

To run this module on its own run the following code: (Replacing 'XXX' with your values)

```
terraform apply -var "env=XXX" \
                -var "aws_access_key=XXX" \
                -var "aws_secret_key=XXX" \
                -var "slack_alert_sns_arn=XXX"
```