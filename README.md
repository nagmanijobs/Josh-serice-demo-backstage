# Josh-service-demo

This service was created from the .NET Hello World on ECS Backstage template.

## Run locally

```bash
dotnet restore
dotnet run --project src/Josh-service-demo/Josh-service-demo.csproj
```

The API listens on port `8080`.

## Endpoints

- `GET /`
- `GET /health`

## Build container image

```bash
docker build -t josh-service-demo:local .
docker run --rm -p 8080:8080 josh-service-demo:local
```

## Deploy to ECS

1. Create ECR repository `dotnet-hello-world` if it does not exist.
2. Build and push image to:
   `123456789012.dkr.ecr.us-east-1.amazonaws.com/dotnet-hello-world:latest`
3. Register task definition from `ecs/task-definition.json`.
4. Update ECS service `my-dotnet-service` in cluster `my-ecs-cluster`.

Example commands:

```bash
aws ecs register-task-definition --cli-input-json file://ecs/task-definition.json --region us-east-1
aws ecs update-service \
  --cluster my-ecs-cluster \
  --service my-dotnet-service \
  --force-new-deployment \
  --region us-east-1
```
