### Test python app locally with Docker
- Build docker image
```bash
cd python-simple-app
docker build --tag my-python-app .
```

- Run the application container from newly created image
```bash
docker run --name python-app -p 8888:8080 my-python-app
```
- Test your application locally
```bash
curl localhost:8888
```

### Automate with Jenkins pipeline
- Install Docker plugins

- Enable Docker service on master
```bash
systemctl enable docker
systemctl start docker
```

- Grant Docker socket permission to Jenkins user
```bash
usermod -a -G docker jenkins
systemctl restart jenkins
```

### Create Pipeline job for testing Nodejs
