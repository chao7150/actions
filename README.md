# Shared GitHub Actions

Reusable workflows for GitHub Actions.

## ECR Push Workflow

Push Docker images to Amazon ECR.

### Usage

```yaml
jobs:
  docker-build-and-push:
    name: Build and Push to ECR
    uses: chao7150/actions/.github/workflows/ecr-push.yml@main
    secrets:
      aws_role_to_assume: ${{ secrets.AWS_ROLE_TO_ASSUME }}
    with:
      aws_region: ${{ vars.AWS_REGION }}
      ecr_repository: ${{ vars.ECR_REPOSITORY }}
      docker_context: '.'
      docker_file: './Dockerfile'
```

### Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `aws_region` | AWS Region | Yes | - |
| `ecr_repository` | ECR Repository name | Yes | - |
| `docker_context` | Docker build context path | No | `.` |
| `docker_file` | Dockerfile path | No | - |

### Secrets

| Name | Description | Required |
|------|-------------|----------|
| `aws_role_to_assume` | AWS IAM Role ARN to assume | Yes |

### Required Permissions

The calling workflow must have:

```yaml
permissions:
  id-token: write
  contents: read
```
