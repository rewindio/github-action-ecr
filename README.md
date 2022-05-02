# github-action-ecr

This is a reusable workflow that builds and publishes an image to ECR.

## Example usage

```yaml
name: ECR
concurrency: ecr

on:
  push:

jobs:
  publish:
    name: "ECS-ECR"
    uses: rewindio/github-action-ecr/.github/workflows/publish.yml@v0
    with:
      profile: production
      ecr_repository: my-ecr-repo
      regions: |
       ["us-east-1"]
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      GITHUB_PAT: ${{ secrets.GITHUB_PAT }}
```

