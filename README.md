# ▬▬▬▬ஜ۩ Install a runner - Linux ۩ஜ▬▬▬▬

![Logo](https://raw.githubusercontent.com/id1945/angular-gitlab-cicd-nginx/master/runner-token.png)

### ☠ Download the binary for your system
```bash
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
```

### ☠ Give it permissions to execute
```bash
sudo chmod +x /usr/local/bin/gitlab-runner
```

### ☠ Create a GitLab CI user
```bash
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash
```

### ☠ Install and run as service
```bash
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
sudo gitlab-runner start
```

### ☠ Command to register runner
```bash
sudo gitlab-runner register --url https://gitlab.com/ --registration-token $REGISTRATION_TOKEN
```

### ☠ Preparing the "shell" executor
```bash
sudo gitlab-runner run
```

## ✍ Setup sudo password
```bash
$ sudo usermod -a -G sudo gitlab-runner
$ sudo visudo
gitlab-runner ALL=(ALL) NOPASSWD: ALL
```