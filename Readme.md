# MERN Stack Kubernetes Deployment with Jenkins CI/CD

A complete MERN (MongoDB, Express.js, React.js, Node.js) stack application deployed on Amazon EKS using Helm charts and Jenkins CI/CD pipeline.

## 🏗️ Architecture Overview

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   React Frontend│    │  Express Backend│    │    MongoDB      │
│   (Port 3000)   │◄──►│   (Port 3000)   │◄──►│   (Port 27017)  │
│   LoadBalancer  │    │   ClusterIP     │    │   ClusterIP     │
└─────────────────┘    └─────────────────┘    └─────────────────┘
        │                       │                       │
        └───────────────────────┼───────────────────────┘
                                │
                    ┌─────────────────┐
                    │   Amazon EKS    │
                    │   Cluster       │
                    └─────────────────┘
```

## 📁 Project Structure

```
Hero-Vired-Kubernetes-helm-jenkins-assignment/
├── learnerReportCS_backend/          # Node.js/Express backend
│   ├── controllers/
│   ├── database/
│   │   └── mongoDb.js               # MongoDB connection
│   ├── models/
│   ├── routes/
│   ├── Dockerfile
│   ├── index.js                     # Main server file
│   └── package.json
├── learnerReportCS_frontend/         # React frontend
│   ├── src/
│   ├── public/
│   ├── Dockerfile
│   └── package.json
├── mongodb/                          # MongoDB Kubernetes manifests
│   ├── mongodb-deployment.yaml
│   └── mongodb-service.yaml
├── helm/mern-chart/                 # Helm chart for application
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
│       ├── backend-deployment.yaml
│       ├── backend-service.yaml
│       ├── frontend-deployment.yaml
│       └── frontend-service.yaml
├── jenkins/
│   └── jenkinsfile                  # CI/CD pipeline
└── README.md
```

## 🚀 Features

- **Containerized MERN Stack**: Docker containers for frontend and backend
- **Kubernetes Orchestration**: Deployed on Amazon EKS cluster
- **Helm Package Management**: Organized deployments with Helm charts
- **Jenkins CI/CD**: Automated build, test, and deployment pipeline
- **Auto-scaling**: Kubernetes deployments with replica management
- **Load Balancing**: AWS LoadBalancer for frontend traffic
- **Service Discovery**: Internal service communication via Kubernetes DNS
- **Environment Management**: Configurable environment variables
- **Health Monitoring**: Built-in health checks and monitoring

## 🛠️ Technology Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Frontend** | React.js, Node.js | User interface |
| **Backend** | Express.js, Node.js | REST API server |
| **Database** | MongoDB | Data persistence |
| **Container** | Docker | Application packaging |
| **Orchestration** | Kubernetes (EKS) | Container orchestration |
| **Package Manager** | Helm | Kubernetes deployments |
| **CI/CD** | Jenkins | Automated pipeline |
| **Cloud** | AWS (EKS, ELB) | Infrastructure |

## 📋 Prerequisites

- AWS Account with EKS cluster setup
- Jenkins server with required plugins
- Docker Hub account
- kubectl configured for EKS cluster
- Helm 3.x installed

### Required Jenkins Plugins
- AWS Credentials Plugin
- Docker Plugin
- Kubernetes CLI Plugin
- Pipeline Plugin

## 🔧 Setup Instructions

### 1. Clone Repository
```bash
git clone https://github.com/XXRadeonXFX/Hero-Vired-Kubernetes-helm-jenkins-assignment.git
cd Hero-Vired-Kubernetes-helm-jenkins-assignment
```

### 2. Configure Jenkins Credentials

Create the following credentials in Jenkins:

#### Docker Hub Credentials
- **ID**: `DOCKER-PRINCE-CRED`
- **Type**: Username with password
- **Username**: Your Docker Hub username
- **Password**: Your Docker Hub password

#### AWS Credentials  
- **ID**: `PRINCE-AWS-CRED`
- **Type**: AWS Credentials
- **Access Key ID**: Your AWS access key
- **Secret Access Key**: Your AWS secret key

### 3. Update Configuration Files

#### Update values.yaml
Edit `helm/mern-chart/values.yaml`:

```yaml
backend:
  name: learner-backend
  image: your-dockerhub-username/learner-backend:latest
  replicas: 1
  port: 3000
  service:
    type: ClusterIP
    port: 3000
    targetPort: 3000
  env:
    - name: NODE_ENV
      value: "production"
    - name: ATLAS_URI  # Backend looks for this variable
      value: "mongodb://mongodb-service.database.svc.cluster.local:27017/learnerdb"
    - name: MONGODB_URI  # Backup variable
      value: "mongodb://mongodb-service.database.svc.cluster.local:27017/learnerdb"

frontend:
  name: learner-frontend
  image: your-dockerhub-username/learner-frontend:latest
  replicas: 1
  port: 3000
  service:
    type: LoadBalancer
    port: 80
    targetPort: 3000
  env:
    - name: REACT_APP_API_URL
      value: "http://learner-backend-service:3000"
```

#### Update Jenkinsfile
Edit `jenkins/jenkinsfile` environment variables:

```groovy
environment {
  DOCKER_USERNAME = "your-dockerhub-username"
  BACKEND_IMAGE   = "${DOCKER_USERNAME}/learner-backend:latest"
  FRONTEND_IMAGE  = "${DOCKER_USERNAME}/learner-frontend:latest"
  CLUSTER_NAME    = "your-eks-cluster-name"
  REGION          = "your-aws-region"
}
```

## 🚀 Deployment

### Option 1: Jenkins Pipeline (Recommended)

1. Create a new Pipeline job in Jenkins
2. Configure SCM to point to your repository
3. Set Pipeline script path to `jenkins/jenkinsfile`
4. Run the pipeline

### Option 2: Manual Deployment

#### Deploy MongoDB
```bash
kubectl create namespace database
kubectl apply -f mongodb/mongodb-deployment.yaml -n database
kubectl apply -f mongodb/mongodb-service.yaml -n database
```

#### Build and Push Images
```bash
# Backend
cd learnerReportCS_backend
docker build -t your-username/learner-backend:latest .
docker push your-username/learner-backend:latest

# Frontend  
cd ../learnerReportCS_frontend
docker build -t your-username/learner-frontend:latest .
docker push your-username/learner-frontend:latest
```

#### Deploy Application
```bash
cd helm/mern-chart
helm upgrade --install learner-app . \
  --namespace default \
  --set backend.image=your-username/learner-backend:latest \
  --set frontend.image=your-username/learner-frontend:latest
```

## 🔍 Verification

### Check Pod Status
```bash
# Application pods
kubectl get pods -n default

# MongoDB pods
kubectl get pods -n database
```

### Check Services
```bash
kubectl get services -n default
kubectl get services -n database
```

### Check Logs
```bash
# Backend logs
kubectl logs deployment/learner-backend -n default

# Frontend logs  
kubectl logs deployment/learner-frontend -n default

# MongoDB logs
kubectl logs deployment/mongodb -n database
```

### Access Application
```bash
# Get frontend URL
kubectl get service learner-frontend-service -n default
```

## 🐛 Troubleshooting

### Common Issues

#### 1. Backend Connection Error
**Error**: `querySrv ENOTFOUND _mongodb._tcp.cluster0.aorqndq.mongodb.net`

**Solution**: The backend is looking for `ATLAS_URI` environment variable. Update your values.yaml:
```yaml
env:
  - name: ATLAS_URI
    value: "mongodb://mongodb-service.database.svc.cluster.local:27017/learnerdb"
```

#### 2. Image Pull Errors
**Error**: `ErrImagePull` or `ImagePullBackOff`

**Solutions**:
- Verify Docker Hub credentials in Jenkins
- Check image names and tags
- Ensure images are public or credentials are configured

#### 3. MongoDB Connection Issues
**Error**: Backend can't connect to MongoDB

**Solutions**:
```bash
# Test MongoDB connectivity
kubectl run mongodb-test --image=mongo:5.0 --rm -i --restart=Never --namespace=database -- \
  mongo --host mongodb-service.database.svc.cluster.local:27017 --eval "db.adminCommand('ping')"

# Check MongoDB logs
kubectl logs deployment/mongodb -n database
```

#### 4. Service Discovery Issues
**Error**: Services can't communicate

**Solutions**:
```bash
# Check DNS resolution
kubectl exec deployment/learner-backend -n default -- nslookup mongodb-service.database.svc.cluster.local

# Verify service endpoints
kubectl get endpoints -n default
kubectl get endpoints -n database
```

### Debug Commands

```bash
# Describe problematic pods
kubectl describe pod <pod-name> -n <namespace>

# Get detailed events
kubectl get events --sort-by=.metadata.creationTimestamp -n default

# Check resource usage
kubectl top pods -n default
kubectl top nodes

# Helm debugging
helm status learner-app -n default
helm get values learner-app -n default
```

## 📊 Monitoring

### Pod Health
```bash
# Check pod status
kubectl get pods -n default -o wide

# Check pod resource usage
kubectl top pods -n default
```

### Service Health
```bash
# Test backend API
kubectl port-forward service/learner-backend-service 3000:3000 -n default
curl http://localhost:3000

# Test MongoDB connection
kubectl port-forward service/mongodb-service 27017:27017 -n database
mongo mongodb://localhost:27017
```

## 🔒 Security Considerations

- MongoDB deployed without authentication (development only)
- Container images should be scanned for vulnerabilities
- Kubernetes RBAC should be configured for production
- Network policies can be added for additional security
- Secrets should be used for sensitive data instead of ConfigMaps

## 🚦 Pipeline Stages

The Jenkins pipeline includes the following stages:

1. **Checkout Code**: Clone repository
2. **Configure AWS CLI**: Setup EKS access
3. **Build & Push Backend**: Docker build and push
4. **Build & Push Frontend**: Docker build and push  
5. **Deploy MongoDB**: Deploy database if needed
6. **Clean Existing Deployments**: Remove old versions
7. **Deploy Application**: Helm deployment
8. **Post-deployment**: Verification and cleanup

## 🌐 Access URLs

After successful deployment:

- **Frontend**: Available via LoadBalancer external IP
- **Backend API**: `http://learner-backend-service:3000` (internal)
- **MongoDB**: `mongodb://mongodb-service.database.svc.cluster.local:27017` (internal)

## 📝 Development Workflow

1. Make code changes
2. Commit and push to repository
3. Jenkins automatically triggers pipeline
4. Pipeline builds, tests, and deploys
5. Verify deployment health
6. Monitor application performance

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License.

## 📞 Support

For issues and questions:
- Create an issue in the GitHub repository
- Check the troubleshooting section above
- Review Jenkins pipeline logs
- Examine Kubernetes events and logs

---

**Note**: This is a development/learning setup. For production use, additional security, monitoring, and high-availability configurations should be implemented.
