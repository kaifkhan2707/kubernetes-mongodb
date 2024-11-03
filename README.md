# Architecture
![Architecture Diagram](/img/architecture.png)

# Architecture Overview:
**MongoDB Deployment on Kubernetes**:

MongoDB is deployed in a Kubernetes cluster, with Docker Desktop used to run the containers. Kubernetes orchestrates the MongoDB pod, providing scalability and fault tolerance.

**Kubernetes Secrets for Credentials:**

MongoDB credentials (such as username and password) are stored securely using Kubernetes Secrets. This ensures sensitive information is not exposed in plain text within configuration files or environment variables.

**MongoDB Pod:**

This is the actual MongoDB database container, running as a Kubernetes pod.
It manages the storage and retrieval of data for applications.

**MongoDB Internal Service:**

An internal Kubernetes service (ClusterIP) that enables other pods within the same Kubernetes cluster to communicate with the MongoDB pod.
This service abstracts the direct pod IP, providing stable internal access to MongoDB.

**Mongo Express Pod:**

Mongo Express is a web-based administrative interface for MongoDB, also running in its own Kubernetes pod.
This pod connects to MongoDB through the internal service, allowing users to interact with MongoDB databases through a web UI.

**Mongo Express External Service:**

An external Kubernetes service (LoadBalancer type) exposes the Mongo Express application to the outside world.
The load balancer routes external HTTP traffic to the Mongo Express pod, allowing users to access the Mongo Express UI via a web browser.

**Flow of Communication:**

User Access: Users access the Mongo Express UI through the external load balancer service.

Mongo Express Pod: The external service routes traffic to the Mongo Express pod.

Internal Database Communication: Mongo Express interacts with MongoDB via the internal service, allowing users to view and manage databases.
