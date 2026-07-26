# tf-import-gen

> Adopt the infrastructure you already have without hand-typing import blocks.

**Status:** 🚧 In development

## Overview

Generate Terraform import blocks for resources that already exist in a cloud account, so adopting unmanaged infrastructure stops being hand-written HCL.

## Features

- Discovers live resources and emits Terraform 1.5 `import {}` blocks with the right `id` format per resource type
- Skips anything already tracked in the current state file, so re-runs stay idempotent
- Filters discovery by resource type, region and tag so you adopt one slice at a time
- Generates `for_each` keyed addresses instead of dozens of numbered ones where the set is obvious
- Pairs with `terraform plan -generate-config-out` and can write the placeholder config itself
- Writes one `imports.tf` or splits per target module

## Stack

Go + `aws-sdk-go-v2`, `hashicorp/hcl/v2` (hclwrite) for HCL generation, `hashicorp/terraform-exec` to read state, cobra.

## Usage

```bash
tf-import-gen aws --region eu-west-1 \
  --types aws_s3_bucket,aws_iam_role --tag Owner=platform \
  --to-module module.platform --out imports.tf
```

## License

MIT
