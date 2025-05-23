# Kubernetes Ingress Example with NGINX

This project demonstrates how to configure an NGINX Ingress Controller in a local Minikube Kubernetes cluster to serve multiple micro-sites:

- `/` → Main landing page
- `/jacket` → Jacket page
- `/boots` → Boots page

## 💻 Structure

Each site is a standalone NGINX container serving a simple HTML page:

- `main-site/` — Home page with links to jacket and boots
- `jacket-site/` — Jacket landing page
- `boots-site/` — Boots landing page

All containers are deployed as Pods and exposed via Services in the `ingress-nginx` namespace.

## 📦 Steps to run locally

1. Enable Ingress addon in Minikube:

```bash
minikube addons enable ingress

2. Build Docker images

docker build -t azakg/main-site:latest ./main-site
docker build -t azakg/jacket-site:latest ./jacket-site
docker build -t azakg/boots-site:latest ./boots-site

3. Push to Docker Hub:
docker push azakg/main-site:latest
docker push azakg/jacket-site:latest
docker push azakg/boots-site:latest

4. Apply Kubernetes resources:

kubectl apply -f main.yaml
kubectl apply -f jacket.yaml
kubectl apply -f boots.yaml
kubectl apply -f ingress.yaml


5. Start tunnel:
sudo minikube tunnel


6. Open in browser:
http://127.0.0.1/  - This main page
http://127.0.0.1/jacket -- This is jacket page
http://127.0.0.1/boots  -- This is boots page

