
>[!info]
>This file is located at `.github/workflows/build-push-deploy.yml`


```yaml
name: Deploy Game Services to GitHub Container Registry

on:
  workflow_dispatch:

env:
  REGISTRY: ghcr.io
  REPO_NAME: "ghcr.io/alderoberge/agx"
  COMPOSE_FILE: "AGX-Server/docker-compose.yml"
  IMAGE_NAME: ${{ github.repository }}

jobs:
  build-and-push:
    name: Build and Push Docker Image via docker-compose
    runs-on: ubuntu-latest
    environment: Testing
    
    permissions:
      contents: read
      packages: write
    
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."

      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Log in to GitHub Container Registry
        uses: docker/login-action@v3
        with:
          registry: ${{ env.REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Build Docker Images via docker compose
        run: docker compose -f ${{ env.COMPOSE_FILE }} build

      - name: Extract metadata (tags, labels) for Docker
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}

      - name: Build and Push using Docker Compose
        run: |
          docker compose -f ${{ env.COMPOSE_FILE }} build
          docker compose -f ${{ env.COMPOSE_FILE }} push

  # The following does not work at the moment
  deploy-to-testing:
    name: Deploy to Testing Environment
    runs-on: ubuntu-latest
    needs: build-and-push
    environment: Testing
    steps:
      - name: Deploy using SSH and docker-compose
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.SSH_HOST_TEST }}
          username: ${{ secrets.SSH_USER_TEST }}
          key: ${{ secrets.SSH_PRIVATE_KEY_TEST }}
          port: 22
          script: |
            echo "Navigating to deployment directory..."
            cd /path/to/your/deployment-directory
            echo "Pulling latest Docker images..."
            docker compose -f docker-compose.yml pull
            echo "Recreating containers..."
            docker compose -f docker-compose.yml up -d
            echo "Deployment to testing environment complete."

```


# Steps

## 1. Building and pushing images

This workflow file does not require any special secrets to build the image, since it's ran on a GitHub Action Runner. :LiSmile:

### 2. Automatic Deployment to Server

>[!warning] WIP
> The deployment step is non functional at the moment.

Required secrets : 

| Key                  | Example Value |
| -------------------- | ------------- |
| SSH_HOST_TEST        | example.com   |
| SSH_USER_TEST        | user          |
| SSH_PRIVATE_KEY_TEST | private key   |

