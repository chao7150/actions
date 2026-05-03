# Shared GitHub Actions

Reusable workflows for GitHub Actions.

## ECR Push Workflow

Push Docker images to Amazon ECR and trigger PR creation for tag updates.

### Usage

```yaml
jobs:
  docker-build-and-push:
    name: Build and Push to ECR
    uses: chao7150/actions/.github/workflows/ecr-push.yml@main
    permissions:
      id-token: write
      contents: read
    secrets:
      aws_role_to_assume: ${{ secrets.AWS_ROLE_TO_ASSUME }}
      dispatch_token: ${{ secrets.DISPATCH_TOKEN }}
    with:
      aws_region: ${{ vars.AWS_REGION }}
      ecr_repository: ${{ vars.ECR_REPOSITORY }}
```

### Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `aws_region` | AWS Region | Yes | - |
| `ecr_repository` | ECR Repository name | Yes | - |
| `docker_context` | Docker build context path | No | `.` |
| `docker_file` | Dockerfile path | No | - |
| `dispatch_enabled` | Enable repository dispatch for PR creation | No | `true` |
| `dispatch_repository` | Target repository for dispatch | No | `chao7150/sakura2-iac` |

### Secrets

| Name | Description | Required |
|------|-------------|----------|
| `aws_role_to_assume` | AWS IAM Role ARN to assume | Yes |
| `dispatch_token` | PAT for repository dispatch | No (required if dispatch_enabled=true) |

### Required Permissions

```yaml
permissions:
  id-token: write
  contents: read
```

### Setup

1. Create a Fine-grained PAT with `contents:write` and `pull_requests:write` permissions for `sakura2-iac`
2. Add the PAT as `DISPATCH_TOKEN` secret in each repository using this workflow
