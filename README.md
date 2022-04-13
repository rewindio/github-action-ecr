# github-action-ecs-deploy

This is a reusable workflow that both publishes images to ECR and deploys them to ECS.

This deployment is opinionated and only renders a single container definition at a time. Rendering multiple container definitions in a single deploy is possible but challenging given the constraints of reusable workflows in GitHub Actions.

## Example usage

```yaml
name: ECS
concurrency: ecs

on:
  push:

jobs:
  deploy:
    name: "ECR-ECS"
    uses: rewindio/github-action-ecs-deploy/.github/workflows/publish-and-deploy.yml@v0
    with:
      aws_region: ca-central-1
      ecs_cluster_name: my-cluster
      ecs_service_name: my-Service-6XXXMsrEhjXH
      ecs_task_definition: my-task-definition
      ecs_container_definition: my-container-definition
      ecr_repository: my-ecr-repo-name
      ecr_push: ${{ github.ref == 'refs/heads/main' }}
      ecs_deploy: ${{ github.ref == 'refs/heads/main' }}
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

