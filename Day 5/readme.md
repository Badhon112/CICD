## Build, Push & Deploy a Dockerize Flask App with Jenkins | Project-Based Approach

- Agenda :
  - Set up DooD in Jenkins
  - build a Dockerize Flask app and push to a private registry

DooD = Docker Out Side Of Docker

## Step 2: Allow the Jenkins user to talk to the socket

The docker cli what is responsible to control the docker demon it located in
/var/run/docker.sock

docker.sock

we need to mound the docker.sock to the jenkins container

so lets find the docker.sock

```bash
docker run -d --name jenkins --restart unless-stopped \
	-p 8080:8080 -p 50000:50000 \
	-v jenkins_home:/var/jenkins_home \
	-v /var/run/docker.sock:/var/run/docker.sock \
	-e TZ=Asia/Dhaka \
	jenkins/jenkins:lts
```

to access the docker.sock file we need to change the permision of that file that why we need $sudo chmod 666 /var/run/docker.sock

## Step 3: Install the Docker CLI inside the Jenkins container

- We’re installing only the client, not a daemon.

```bash
docker exec -u root -it jenkins bash -lc \
  'curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh'
```

## Step 4: Verify from inside Jenkins

```bash
docker exec -it jenkins bash -lc 'docker version && docker ps'
```

Demo — Build, Push & Deploy a Flask App with Jenkins (DooD)

## Step 5: Set Up jenkins and docker hub with git private repo

- Now create a GitHub token to access the private repo
  - Go to setting -> Developer -> Create a access token

- Now in jenkins create a jobs copy the url of github private repo set the token into the github repo.
- Now in Build Steps in Execute Shell
  - Run this command

- In the Environment use secret text(s) or file(s)
  - Select Username and password(separated)

```bash
# 1) Docker login (uses injected env vars)
echo "Logging in to Docker Hub..."
echo "$DOCKERHUB_PWD" | docker login -u "$DOCKERHUB_USER" --password-stdin

# 2 ) Image naming
IMAGE='badhon58/frontend'
TAG="${BUILD_NUMBER}"

# 3) Build and push (exact tag + latest for convenience)
echo "Building image..."
docker build -t "$IMAGE:$TAG" -t "$IMAGE:latest" .

echo "Pushing Image..."
docker push "$IMAGE:$TAG"
docker push "$IMAGE:latest"

# 4) Deploy on the Docker host (DooD)
echo "Deploying..."
docker pull "$IMAGE:$TAG"
docker rm -f frontend || true
docker run -d --name frontend -p 3000:3000 "$IMAGE:$TAG"
```

<!-- Success  -->