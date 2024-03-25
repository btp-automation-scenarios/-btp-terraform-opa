# BTP  Terraform and Open Policy Agent (OPA) Integration

Sample repository for showcasing Open Policy Integration with Terraform.

## Steps to run the code

```bash	
cd infra
terraform init
terraform plan --out tfplan.binary
terraform show -json tfplan.binary > tfplan.json
```

## Steps to run the OPA policy

In the root folder execute the following command to evaluate the result of the policy:

```bash
opa exec --decision terraform/analysis/autoexec --bundle policy/ ./infra/tfplan.json
```

To get more details about the OPA policy scoring:

```bash
opa exec --decision terraform/analysis/score --bundle policy/ ./infra/tfplan.json
```

To fetch the result from the JSON you can pipe it to `jq`:

```bash
opa exec --decision terraform/analysis/autoexec --bundle policy/ ./infra/tfplan.json | jq '.result[].result'
opa exec --decision terraform/analysis/score --bundle policy/ ./infra/tfplan.json | jq '.result[].result' regoresult.json
```

