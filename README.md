# ஜ۩ Install a runner - Linux ۩ஜ

![Logo](https://raw.githubusercontent.com/id1945/angular-gitlab-cicd-nginx/master/runner-token.png)
![Logo](https://raw.githubusercontent.com/id1945/angular-gitlab-cicd-nginx/master/pieline.png)

### .gitlab-ci.yml

```yml
stages:          # List of stages for jobs, and their order of execution
  - build
  - deploy

build-job:       # This job runs in the build stage, which runs first.
  stage: build
  tags:
    - angularci
  script:
    - echo "Compiling the code..."
    - npm i
    - npm run build
    - echo "Compile complete."
  artifacts:
    expire_in: 1 hour
    paths:
      - dist
  only: 
    - master

deploy-job:      # This job runs in the deploy stage.
  stage: deploy  # It only runs when *both* jobs in the test stage complete successfully.
  tags:
    - angularci
  script:
    - echo "Deploying application..."
    - chmod +x deploy.sh
    - bash deploy.sh
    #- sudo rm -rf /usr/share/nginx/html/*
    #- sudo cp -rv dist/angular-ci/* /usr/share/nginx/html
    - echo "Application successfully deployed."
  only: 
    - master
```

### ⌛ [1] Download the binary for your system
```bash
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
```

### ⌛ [2] Give it permissions to execute
```bash
sudo chmod +x /usr/local/bin/gitlab-runner
```

### ⌛ [3] Create a GitLab CI user
```bash
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash
```

### ⌛ [4] Install and run as service
```bash
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
sudo gitlab-runner start
```

### ⌛ [5] Command to register runner
```bash
sudo gitlab-runner register --url https://gitlab.com/ --registration-token $REGISTRATION_TOKEN
```

### ⌛ [6] Preparing the "shell" executor
```bash
sudo gitlab-runner run
```

## ✍ Setup sudo password
```bash
$ sudo usermod -a -G sudo gitlab-runner
$ sudo visudo
gitlab-runner ALL=(ALL) NOPASSWD: ALL
```