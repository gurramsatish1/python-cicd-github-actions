# Python CI/CD with GitHub Actions

This repository demonstrates how to set up a simple CI/CD pipeline for a Python Flask application using GitHub Actions and Docker.

## Features
- Run tests using pytest
- Build and push Docker image to Docker Hub
- GitHub Actions workflow triggered on every push to `main`

## Run Locally

```bash
pip install -r requirements.txt
python app.py
```

## Deploy to Kubernetes

The Helm chart in `helm-chart/` is configured to use the Docker Hub image `satishgurram/python-cicd:3e7487f105d348aec78e5146d6274e3606bfb871`.

To install on any cluster (including AKS) you can run:

```bash
kubectl create namespace python-app # optional
helm upgrade --install python-app helm-chart \
  --namespace python-app \
  --set image.repository=satishgurram/python-cicd \
  --set image.tag=3e7487f105d348aec78e5146d6274e3606bfb871
```

When you build a new image, update the `image.tag` value above or in `helm-chart/values.yaml`, then re‑run the command to deploy the new version.
