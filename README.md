# How to
---

## prerequisite
- [docker desktop](https://www.docker.com/products/docker-desktop/) or [docker engine](https://docs.docker.com/engine/)

## project description
This project is created for docker learning purpose

**project structure**
```bash
.
├── api
│   ├── api/
│   ├── main/
│   ├── Dockerfile
│   ├── entrypoint.sh
│   ├── manage.py
│   └── requirements.txt
├── compose.yml
└── README.md
```

- `api`: django app source
- `Dockerfile`: for build image
- `entrypoint.sh`: entrypoint for Dockerfile
- `compose.yml`: services defined files


## steps
1. Clone this app to your local machine and change to project directory
```bash
git clone https://github.com/xavier-golden-owl/simple-docker-demo
cd simple-docker-demo
```

2. build and run this app using docker command
```bash
docker compose up -d --build
```
parameters:
- `--build`: build 
- `-d`: run in [detach mode](https://docs.docker.com/engine/reference/run/#:~:text=new%20container%20id-,Detached%20(%2Dd),specify%20the%20%2D%2Drm%20option.)
- if you separate docker compose file for (dev / staging / prod environment), changae compose.yml to your target compose file
	- docker compose -f **compose.yml** -d --build

3. Open you browser and navigate to: [http://localhost:8000](http://localhost:8000) to monitor the results



## troubleshooting
**watch logs**
```bash
docker compose logs -f
```
parameters:
- `-f`: follow logs (realtime)

### 1. cannot start django server
1. Navigate to compose.yml file
2. Change port mapping to your web service
```yaml
services:
  web:
    ...
    ports:
      - <available_port>:8000
  db:
    ...
```

change <available_port> to any port that available in your host machine

### 1. cannot connect to postgres database
1. Navigate to compose.yml file
2. Add port mapping to your db service
```yaml
services:
  web:
    ...
  db:
    ...
    ports:
      - <available_port>:5432
```

change <available_port> to any port that available in your host machine
