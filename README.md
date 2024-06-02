# tilt docker kubernetes

- https://tilt.dev/

- Install Tilt:
```bash
curl -fsSL https://raw.githubusercontent.com/tilt-dev/tilt/master/scripts/install.sh | bash 
```

- Install tilt with wget
```bash
wget https://github.com/tilt-dev/tilt/releases/download/v0.33.14/tilt.0.33.14.linux.x86_64.tar.gz
tar -xvf tilt.0.33.14.linux.x86_64.tar.gz
sudo mv tilt /usr/local/bin/tilt
```

- docker project structure
```bash
flask-app/
├── Dockerfile
├── requirements.txt
├── app.py
└── Tiltfile
```

- docker compose
```bash
docker compose -p flask-app up -d --build
```

- tilt up
```bash
tilt up
```

- kubernetes project structure
```bash
flask-app/
├── app.py
├── Dockerfile
├── requirements.txt
├── Tiltfile
└── charts/
    └── flask-app/
        ├── Chart.yaml
        ├── values.yaml
        ├── .helmignore
        ├── templates/
        │   ├── deployment.yaml
        │   ├── service.yaml
        │   ├── ingress.yaml
        │   └── ...
        └── charts/
```

- private registry secrets, I am using dockerhub
```bash
kubectl create ns flask-app
kubectl create secret docker-registry docker-registry \
  --docker-server=https://index.docker.io/v1/ \
  --docker-username=dockerhub id \
  --docker-password=token \
  --docker-email=your-email \
  --namespace=flask-app
```

```bash 
- kubernetes tilt file
```tilt
# In your Tiltfile
k8s_yaml(helm('./charts/flask-app'))
```

- First Manuanl Steps build and push (local laptop)
```bash
docker login
docker build -t chasim1982/flask-app:v1 .
docker push chasim1982/flask-app:v1
```
- Helm install
```bash
helm -n flask-app upgrade --install flask-app --create-namespace ./charts/flask-app -f ./charts/flask-app/values.yaml --wait
```

- Tilt up
```bash
tilt up
```