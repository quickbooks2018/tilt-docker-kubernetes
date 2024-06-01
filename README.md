# tilt docker kubernetes

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

- project structure
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