# tfstate S3 bucket Terraform config

This set of configs creates an S3 bucket for storing Terraform state.
This config's Terraform state files aren't stored anywhere, so consider this configs as one-shot tool to create a bucket and a secret with bucket access tokens in Yandex Vault.

Usage:
1. `export YC_STAGE="preprod"  # possible stages: preprod prod testing`
2. `$ ./terraform.sh -s ${YC_STAGE} init`
3. `$ ./terraform.sh -s ${YC_STAGE} apply`
4. Look for new secret with name like 'yc-walle-${YC_STAGE}-terraform-state-s3-storage' in https://yav.yandex-team.ru/ .
5. Place this secret ID into variable `TERRAFORM_STATE_STORAGE_YAV_SECRET_ID` in [../yc-prod/terraform.sh](../yc-prod/terraform.sh) / [../yc-preprod/terraform.sh](../yc-preprod/terraform.sh) / [../yc-testing/terraform.sh](../yc-testing/terraform.sh) / etc, along with other stage's variables.
