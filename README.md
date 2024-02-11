# E-Commerce Application Deployment and Debugging

## Overview

This project outlines the deployment process of an e-commerce application on a Kubernetes cluster. The application architecture includes a React-based frontend, Node.js backend APIs, a MongoDB database, and RabbitMQ for message queuing.

## Application Components

- **Frontend**: React application served via Nginx.
- **Backend API**: Node.js microservices.
- **Database**: MongoDB cluster.
- **Message Queue**: RabbitMQ.

## Deployment Phases

### Phase 1: Deployment

#### Configuration and Deployment
Kubernetes manifests for each component are provided, ensuring proper configuration, interconnection, and deployment strategies.

#### Networking
An Ingress controller is configured to expose the frontend service, with internal networking set up for inter-service communication.

#### Persistence
Persistent Volumes and Claims are implemented for MongoDB and RabbitMQ.

#### Security and Compliance
Security policies are enforced using Pod Security Policies or OPA/Gatekeeper.

### Phase 2: Observability and Scaling

#### Monitoring and Logging
Integration with Prometheus and Grafana for monitoring, and ELK stack for centralized logging.

#### Autoscaling
Horizontal Pod Autoscaling is set up for the frontend and backend services, with a discussion on Cluster Autoscaling.

### Phase 3: Debugging & Troubleshooting
Guidance on troubleshooting common issues is provided in the `troubleshooting-guide.md`.

## Setup Instructions

Detailed steps to deploy each component are outlined in the corresponding Kubernetes manifest files. Ensure you have kubectl configured correctly to interact with your Kubernetes cluster.

## Contributing

Contributions to improve the deployment or add features are welcome. Please follow the standard fork and pull request workflow.

## Diagram to be used
```
+----------------------------------------+
|              Ingress Nginx             |
+----------------------+-----------------+
|       Frontend       |    Backend     |
|   +--------------+   |   +--------+   |
|   |              |   |   |        |   |
|   |    React     |   |   | Node.js|   |
|   |              |   |   |Microser|   |
|   +--------------+   |   | vices  |   |
+----------------------+---+--------+---+
                        |
          +-------------|-------------+
          |             |
   +------+--------+    |
   |   MongoDB     |    |
   | (Replica Set) |    |
   +------+--------+    |
          |             |
   +------+--------+    |
   |  RabbitMQ    |     |
   +------+--------+    |
          |             |
   +------+--------+    |
   |  Prometheus  |     |       +------------------------+
   +------+--------+    |       |                        |
          |             |       |    Cluster Autoscaler  |
   +------+--------+    |       |                        |
   |   Grafana    |     |       +------------------------+
   +------+--------+    |
          |             |
   +------+--------+    |
   |    ELK Stack  |    |
   +---------------+    |
                        |
+-----------------------+------------------------+
|                Persistent Volumes               |
+-------------------------------------+-----------+
|              Pod Security Policies         |
+--------------------------------------------+
```

## Architecture Diagram 
```
ecommerce-deployment-debugging/
|-- manifests/
|   |-- frontend-deployment.yaml
|   |-- backend-deployment.yaml
|   |-- mongodb-statefulset.yaml
|   |-- rabbitmq-statefulset.yaml
|   |-- ingress-controller.yaml
|-- config/
|   |-- frontend-configmap.yaml
|   |-- backend-configmap.yaml
|   |-- mongodb-configmap.yaml
|   |-- rabbitmq-configmap.yaml
|   |-- secrets.yaml
|-- networking/
|   |-- ingress.yaml
|   |-- service-discovery.yaml
|-- persistence/
|   |-- mongodb-pv.yaml
|   |-- rabbitmq-pv.yaml
|-- security/
|   |-- pod-security-policies.yaml
|-- observability-scaling/
|   |-- monitoring/
|   |   |-- prometheus.yaml
|   |   |-- grafana.yaml
|   |-- logging/
|   |   |-- elk-stack.yaml
|   |-- autoscaling/
|   |   |-- hpa-frontend.yaml
|   |   |-- hpa-backend.yaml
|   |   |-- cluster-autoscaler.yaml
|-- troubleshooting/
|   |-- frontend-accessibility.yaml
|   |-- backend-db-connectivity.yaml
|   |-- order-processing-delays.yaml
|-- README.md
|-- troubleshooting-guide.md

```