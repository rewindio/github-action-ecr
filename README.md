# github-action-ecs-deploy

This is a reusable workflow that both publishes images to ECR and deploys them to ECS via terraform.

## Example usage

```yaml
name: ECS
concurrency: ecs

on:
  push:

jobs:
  deploy:
    name: "ECS-ECR"
    uses: rewindio/github-action-ecs-deploy/.github/workflows/publish-and-deploy.yml@v0
    with:
      deploy_matrix: |
        [
          { "region": "us-east-1", "workspace": "my-workspace-1", "ecr_repository": "test-repo-1" },
          { "region": "us-east-1", "workspace": "my-workspace-2", "ecr_repository": "test-repo-2" },
        ]
      profile: staging
      terraform_dir: .
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      GITHUB_PAT: ${{ secrets.GITHUB_PAT }}
```

