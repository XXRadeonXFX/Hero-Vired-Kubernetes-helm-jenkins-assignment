Perfect! Based on your \*\*actual directory structure\*\*, here is the updated `README.md` file tailored for your submission.



---



\### ✅ Updated `README.md` (for your `mern-deployment` project)



```markdown

\# MERN Stack Deployment using Kubernetes, Helm, and Jenkins



\## 📚 Project Overview



This project demonstrates deploying a full-stack \*\*MERN application\*\* using:



\- \*\*MongoDB\*\* (running in Kubernetes)

\- \*\*Express.js + Node.js\*\* (Backend)

\- \*\*React.js\*\* (Frontend)

\- \*\*Docker\*\* (for containerization)

\- \*\*Helm\*\* (for packaging/deployment)

\- \*\*Jenkins\*\* (for CI/CD automation)



---



\## 📁 Folder Structure



```



Experiment-1/

├── learnerReportCS\\\_backend/          # Backend source code

├── learnerReportCS\\\_frontend/         # Frontend source code

├── mern-deployment/

│   ├── backend/

│   │   ├── deployment.yaml

│   │   └── service.yaml

│   ├── frontend/

│   │   ├── deployment.yaml

│   │   └── service.yaml

│   ├── helm/

│   │   └── mern-chart/

│   │       ├── Chart.yaml

│   │       ├── values.yaml

│   │       └── templates/

│   │           ├── backend-deployment.yaml

│   │           ├── backend-service.yaml

│   │           ├── frontend-deployment.yaml

│   │           └── frontend-service.yaml

│   └── jenkins/

│       └── Jenkinsfile



````



---



\## 🚀 How to Deploy



\### 🐳 1. Build \& Push Docker Images



```bash

\# Backend

cd learnerReportCS\_backend

docker build -t <dockerhub-username>/learner-backend:latest .

docker push <dockerhub-username>/learner-backend:latest



\# Frontend

cd learnerReportCS\_frontend

docker build -t <dockerhub-username>/learner-frontend:latest .

docker push <dockerhub-username>/learner-frontend:latest

````



---



\### ☸️ 2. Deploy MongoDB in Kubernetes



> You should already have this running as a deployment and service:



```bash

mongodb-service.database.svc.cluster.local:27017/TravelMemory

```



---



\### 📦 3. Deploy with Helm



```bash

cd mern-deployment/helm

helm install mern ./mern-chart

```



To upgrade:



```bash

helm upgrade mern ./mern-chart

```



---



\### 🌐 4. Access the App Locally



\#### Frontend:



```bash

kubectl port-forward svc/learner-frontend 3000:3000

\# Open: http://localhost:3000

```



\#### Backend:



```bash

kubectl port-forward svc/learner-backend 5000:5000

\# Open: http://localhost:5000 or /api/test

```



---



\### ⚙️ 5. CI/CD with Jenkins



The Jenkins pipeline performs:



\* Clone code

\* Build Docker images

\* Push to DockerHub

\* Helm deploy to Kubernetes



\#### Jenkins Setup:



\* Docker + kubectl + Helm installed

\* Jenkins credentials ID: `dockerhub-creds`



```groovy

pipeline {

&nbsp; ...

&nbsp; steps {

&nbsp;   sh 'helm upgrade --install mern ./mern-chart --namespace default'

&nbsp; }

}

```



---



\## 📸 Screenshots Included



| Screenshot                   | Description                     |

| ---------------------------- | ------------------------------- |

| ✅ `kubectl get pods`         | All pods running                |

| ✅ Frontend Login UI          | React app live at port 3000     |

| ✅ Backend Route or Hello Msg | Backend responding on port 5000 |

| ✅ Jenkins Job Output         | CI/CD build + deploy success    |

| ✅ `helm install` output      | Helm deployed without errors    |



Place screenshots under a `screenshots/` folder (optional).



---



\## ✅ Submission Link



GitHub Repo:

🔗 \[https://github.com/your-username/mern-k8s-deployment](https://github.com/your-username/mern-k8s-deployment)



---



\## 🙌 Author



\*\*Prince Thakur\*\*

Hero Vired | Containerization and Container Orchestration Assignment

🗓️ Due: 6 July 2025



```



---



Let me know if you'd like me to:

\- Convert this into `.txt` or `.pdf`

\- Generate a zipped submission folder

\- Push everything to a GitHub repo for you



You're 100% ready to submit now. ✅

```

Perfect! Based on your \*\*actual directory structure\*\*, here is the updated `README.md` file tailored for your submission.



---



\### ✅ Updated `README.md` (for your `mern-deployment` project)



```markdown

\# MERN Stack Deployment using Kubernetes, Helm, and Jenkins



\## 📚 Project Overview



This project demonstrates deploying a full-stack \*\*MERN application\*\* using:



\- \*\*MongoDB\*\* (running in Kubernetes)

\- \*\*Express.js + Node.js\*\* (Backend)

\- \*\*React.js\*\* (Frontend)

\- \*\*Docker\*\* (for containerization)

\- \*\*Helm\*\* (for packaging/deployment)

\- \*\*Jenkins\*\* (for CI/CD automation)



---



\## 📁 Folder Structure



```



Experiment-1/

├── learnerReportCS\\\_backend/          # Backend source code

├── learnerReportCS\\\_frontend/         # Frontend source code

├── mern-deployment/

│   ├── backend/

│   │   ├── deployment.yaml

│   │   └── service.yaml

│   ├── frontend/

│   │   ├── deployment.yaml

│   │   └── service.yaml

│   ├── helm/

│   │   └── mern-chart/

│   │       ├── Chart.yaml

│   │       ├── values.yaml

│   │       └── templates/

│   │           ├── backend-deployment.yaml

│   │           ├── backend-service.yaml

│   │           ├── frontend-deployment.yaml

│   │           └── frontend-service.yaml

│   └── jenkins/

│       └── Jenkinsfile



````



---



\## 🚀 How to Deploy



\### 🐳 1. Build \& Push Docker Images



```bash

\# Backend

cd learnerReportCS\_backend

docker build -t <dockerhub-username>/learner-backend:latest .

docker push <dockerhub-username>/learner-backend:latest



\# Frontend

cd learnerReportCS\_frontend

docker build -t <dockerhub-username>/learner-frontend:latest .

docker push <dockerhub-username>/learner-frontend:latest

````



---



\### ☸️ 2. Deploy MongoDB in Kubernetes



> You should already have this running as a deployment and service:



```bash

mongodb-service.database.svc.cluster.local:27017/TravelMemory

```



---



\### 📦 3. Deploy with Helm



```bash

cd mern-deployment/helm

helm install mern ./mern-chart

```



To upgrade:



```bash

helm upgrade mern ./mern-chart

```



---



\### 🌐 4. Access the App Locally



\#### Frontend:



```bash

kubectl port-forward svc/learner-frontend 3000:3000

\# Open: http://localhost:3000

```



\#### Backend:



```bash

kubectl port-forward svc/learner-backend 5000:5000

\# Open: http://localhost:5000 or /api/test

```



---



\### ⚙️ 5. CI/CD with Jenkins



The Jenkins pipeline performs:



\* Clone code

\* Build Docker images

\* Push to DockerHub

\* Helm deploy to Kubernetes



\#### Jenkins Setup:



\* Docker + kubectl + Helm installed

\* Jenkins credentials ID: `dockerhub-creds`



```groovy

pipeline {

&nbsp; ...

&nbsp; steps {

&nbsp;   sh 'helm upgrade --install mern ./mern-chart --namespace default'

&nbsp; }

}

```



---



\## 📸 Screenshots Included



| Screenshot                   | Description                     |

| ---------------------------- | ------------------------------- |

| ✅ `kubectl get pods`         | All pods running                |

| ✅ Frontend Login UI          | React app live at port 3000     |

| ✅ Backend Route or Hello Msg | Backend responding on port 5000 |

| ✅ Jenkins Job Output         | CI/CD build + deploy success    |

| ✅ `helm install` output      | Helm deployed without errors    |



Place screenshots under a `screenshots/` folder (optional).



---



\## ✅ Submission Link



GitHub Repo:

🔗 \[https://github.com/your-username/mern-k8s-deployment](https://github.com/your-username/mern-k8s-deployment)



---



\## 🙌 Author



\*\*Prince Thakur\*\*

Hero Vired | Containerization and Container Orchestration Assignment

🗓️ Due: 6 July 2025



```



---



Let me know if you'd like me to:

\- Convert this into `.txt` or `.pdf`

\- Generate a zipped submission folder

\- Push everything to a GitHub repo for you



You're 100% ready to submit now. ✅

```



