# Assignment3-3
Introduction to containers

## Github secrets to store docker credentials
![](Screenshot-dockerhub-credentials-in-repositorysecrets.png)

## Docker in Dockerhub repository
![](Screenshot-dockerhub-repository.png)


## Workflow enabling build then push to dockerhub
```

      name: Docker Build and Push to DockerHub
      
      on:
        push:
          branches: [ "main" ]  # Triggers on push to main
      
      jobs:
        build-and-push:
          runs-on: ubuntu-latest
      
          steps:
            - name: Checkout code
              uses: actions/checkout@v4  # Checkout Flask app code
      
            - name: Set up Docker Buildx
              uses: docker/setup-buildx-action@v3  # Optimized Docker build setup
      
            - name: Login to DockerHub
              uses: docker/login-action@v3
              with:
                username: ${{ secrets.DOCKERHUB_USERNAME }}
                password: ${{ secrets.DOCKERHUB_TOKEN }}
      
            - name: Build and Push Docker Image
              uses: docker/build-push-action@v6
              with:
                context: .  # Path to Dockerfile
                push: true  # Push to registry after build
                tags: |
                  ${{ secrets.DOCKERHUB_USERNAME }}/assignment3-3-flask:latest
```


## Assignment
Create a public repository in Github<br/>
Commit your sample flask app to it, along with your Dockerfile & requirements.txt<br/>
Set up a Github workflow such as any pushes to the main branch, will trigger a workflow to build and push your image to your DockerHub registry. <br/>
You can use the following marketplace actions (Example usage: https://github.com/docker/build-push-action): <br/>
- docker/login-action@v3 <br/>
- docker/setup-buildx-action@v3<br/>
- docker/build-push-action@v6<br/>

Do not hardcode any credentials in your workflow file (Make use of Github Secrets and reference it in your workflow)<br/>
Submission: Submit your github repository with your workflow<br/>

