# 027_052_062_739

## GDrive Backup using Docker & Kubernetes

Python script `main2.py` monitors a directory (`backupfiles`), uploads any newly created, modified, or moved files to Google Drive using the Google Drive API. There's a Dockerfile to containerize your application, Docker Compose to manage the Docker container, a shell script (`entrypoint.sh`) to restart the container when changes are detected in the `backupfiles` directory, and Kubernetes manifests for setting up a CronJob to periodically trigger the backup process, and Persistent Volume (PV) and Persistent Volume Claim (PVC) for storing backup files persistently.

### Prerequisites:
- python
- docker
- kubernetes
- docker hub account

### Installation:

1. Clone the repository:
   ```
   git clone https://github.com/AishwaryaLPatil/CC_027_052_062_739.git
   ```

Create google drive api credentials:
Enable google drive api
Head to the google cloud console and create a project. inside the created project 
    choose api and services
    select credentials
    click on create credentials and select OAuth client ID
    select Application type = Desktop app 
    Edit the name and create

download credentials.json file and put in the /backup/app/ folder
[Note the app folder should not already contain token.json]

#### How to provide access google drive for backup:

```
cd /backup/app/
```

```
python3 main.py 
```

token.json will be generated and will be redirected to select the gmail id for backing up

#### How to build docker image:

```
cd /backup/
```

```
docker login
```

```
sudo apt install docker-compose 
(install if not there)
```

```
docker build -t aishwarya166/cc_cronbackup_image:latest .
(u can replace with any repository name created on your docker hub)
```

```
docker push aishwarya166/cc_cronbackup_image:latest
```
```
docker run -d aishwarya166/cc_cronbackup_image:latest
```

#### Schedule kubernetes cronjob:

```
minikube start
```

```
kubectl apply -f pv.yaml
```

```
kubectl apply -f pvc.yaml
```

```
kubectl apply -f cronJob.yaml
```

```
kubectl get cronjobs
```

```
kubectl get pods --watch
```

```
kubectl logs job_name
```

#### For changing updating the contents of the backup folder, 

get the container in which the image is running:
```
docker ps --filter ancestor=aishwarya166/cc_cronbackup_image
```

[Replace the DOCKER_CONTAINER_NAME="your-container-name"]
```
./entrypoint.sh
``` 

### Project Members
- Achala Nayak
- Aishwarya L Patil
- Akshatha MK
- A Geethika Chowdary