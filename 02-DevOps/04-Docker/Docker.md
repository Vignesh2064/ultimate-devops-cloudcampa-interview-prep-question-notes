## 🔹 **Docker – Basic Interview Questions**

1. **What is Docker and why is it used?**

   * Docker is a containerization platform that packages applications and their dependencies into containers, ensuring consistency across environments.

2. **What is a container?**

   * A lightweight, standalone executable that includes everything needed to run an application.

3. **Difference between Docker container and virtual machine?**

   * VM uses a hypervisor and OS per VM. Containers share the host OS and are more lightweight and faster.

4. **What is Docker Hub?**

   * A cloud-based registry to share and access Docker images.

5. **What is the Dockerfile?**

   * A text document that contains instructions to build a Docker image.

6. **Dockerfile vs Docker Compose?**

   * Dockerfile defines how to build an image. Docker Compose is used to define and run multi-container applications.

7. **Basic Docker commands?**

   * `docker build`, `docker run`, `docker ps`, `docker stop`, `docker exec`, `docker logs`, etc.

---

## 🔹 **Docker – Intermediate Questions**

1. **How do you manage persistent data in Docker?**

   * Using **Volumes** and **Bind Mounts**.

2. **Explain multi-stage builds in Docker.**

   * Reduces final image size by separating build and runtime environments.

3. **How do you debug a Docker container?**

   * Use `docker logs`, `docker exec`, `docker inspect`, and health checks.

4. **What is the difference between ENTRYPOINT and CMD?**

   * `ENTRYPOINT` sets the main command to run. `CMD` sets default arguments. `CMD` can be overridden.

5. **How do you pass environment variables into Docker?**

   * Using `-e` flag or `.env` file.

6. **What’s the role of Docker network drivers?**

   * They define how containers communicate: `bridge`, `host`, `overlay`, `macvlan`.

7. **How do you optimize Docker image size?**

   * Use `.dockerignore`, multi-stage builds, minimal base images (`alpine`), and clean up intermediate files.

8. **How do you run a container in the background?**

   * `docker run -d image_name`

---

## 🔹 **Docker – Advanced Questions**

1. **Explain the Docker image layering system.**

   * Each instruction in the Dockerfile creates a new layer; layers are cached for efficiency.

2. **How does Docker handle networking across containers in different hosts?**

   * Via **Docker Swarm**, **Overlay Networks**, or **Kubernetes CNI plugins**.

3. **Security best practices with Docker?**

   * Use trusted images, scan images, drop root privileges, limit container capabilities, use namespaces and AppArmor/SELinux.

4. **How to create custom Docker networks and link containers?**

   * `docker network create custom-net`, then attach with `--network custom-net`.

5. **How does Docker handle resource constraints?**

   * Use `--memory`, `--cpus`, and `cgroup` constraints to limit usage.

6. **What is Docker Swarm?**

   * Native clustering/orchestration tool by Docker. Not as feature-rich as Kubernetes but easier for smaller setups.

7. **How to minimize downtime during Docker container upgrade?**

   * Use **blue-green deployment**, **rolling updates**, or run containers behind a **load balancer**.

8. **Explain Copy-on-Write in Docker.**

   * Docker uses UnionFS; base layers are shared and modified layers are written on top (copy-on-write).

---

## 🔹 **Docker – Real-Time Scenario Based Questions (For 40+ LPA)**

1. **You deployed a Docker container in production, but it’s crashing after some time. How do you debug?**

   * Check `docker logs`, use `docker inspect`, verify `healthcheck`, monitor resource limits, check dependencies and volumes.

2. **You need to deploy a Java + Nginx app with Docker and ensure log rotation. How would you structure it?**

   * Multi-stage Dockerfile, separate Nginx and Java container, use volumes for logs, configure logrotate in base image or Docker logging drivers.

3. **How to ensure a new container doesn’t impact existing microservices?**

   * Use `docker-compose` or Kubernetes with separate namespace, apply canary strategy, and test with `curl` or mock APIs.

4. **If a base image you rely on introduces a vulnerability, how do you handle it across 50+ services?**

   * Automate scanning (using Trivy, Clair), rebuild images using patched base, use CI/CD with notifications.

5. **Your Docker container has performance issues. What tools will you use?**

   * `docker stats`, `top`, `htop`, `iostat`, application-level profiling, check host load, and storage drivers.

6. **Explain how you manage secrets in Docker.**

   * Use **Docker Secrets** (in Swarm), environment variables from Vault/AWS Secrets Manager, or inject them at runtime via sidecars in Kubernetes.

7. **In a CI/CD pipeline, how do you use Docker for testing and deployment?**

   * Build images in Jenkins/GitHub Actions, run unit & integration tests in containers, push to registry, deploy using Helm/K8s.

8. **A Docker image size is 2GB+. How do you reduce it for faster deployments?**

   * Remove unnecessary packages, switch to `alpine`, remove cache and temp files, split build/runtime layers.

---

## 🔹 Bonus: GitHub & DockerHub Integration

1. **How to automate Docker builds with GitHub commits?**

   * Use GitHub Actions to trigger builds on push, and auto-push images to DockerHub.

2. **How to handle rollback of a faulty Docker deployment?**

   * Maintain previous image tags, use `docker-compose` with specific versions, or Helm rollback if using Kubernetes.

---

### ✅ **Must-Have Docker Topics for 40+ LPA Roles**

#### 🔹 1. **Core Fundamentals (Basic – Intermediate)**

* What is Docker and how it differs from Virtual Machines
* Docker architecture: client, daemon, registry, objects
* Dockerfile basics (FROM, RUN, COPY, CMD, ENTRYPOINT, etc.)
* Docker volumes vs bind mounts
* Docker Compose basics and service dependency
* Container lifecycle (create, run, pause, stop, rm)

#### 🔹 2. **Advanced Concepts**

* Multi-stage builds in Dockerfile (optimize image size)
* Creating minimal secure images (Alpine, scratch)
* Docker networking: bridge, host, overlay
* Custom bridge networks and DNS resolution
* Managing secrets in Docker (Docker Swarm secrets, external tools)
* Container logging strategies (stdout/stderr, log drivers)
* Docker health checks and recovery

#### 🔹 3. **Real-Time Troubleshooting & Scenarios**

* How to debug a failing container (`docker logs`, `docker exec`, etc.)
* How to reduce image size (best practices)
* Handling orphaned volumes or zombie containers
* Difference between `CMD` and `ENTRYPOINT` with real impact examples
* Live example: Fixing `permission denied` issue in containerized apps
* Dealing with crashing containers in CI/CD pipelines

#### 🔹 4. **Security-Related Questions**

* How do you scan Docker images for vulnerabilities?
* Docker Bench for Security
* Best practices to run containers as non-root users
* Use of seccomp, AppArmor, and user namespaces

#### 🔹 5. **Docker in CI/CD**

* How to use Docker in Jenkins pipelines (Docker-in-Docker or Docker socket bind mount)
* Building Docker images in a CI/CD pipeline
* Publishing Docker images to ECR/Docker Hub securely

#### 🔹 6. **GitHub Actions + Docker (Bonus)**

* How to use Docker with GitHub Actions for CI/CD
* Sample `.github/workflows/docker-build.yml` pipeline

---

### 📌 Final Tips to Crack High-Paying Docker Interviews

✅ **Prepare 3–5 Real Projects/Use Cases**, like:

* Dockerizing a Python/Node/Java microservice app
* Using Docker Compose for multi-container app
* Creating and pushing optimized Docker images in a Jenkins/GitHub Actions pipeline

✅ **Mock Answers with Real-Time Explanation**
Prepare answers with:

* Problem → What you did → Tools used → Outcome

✅ **Be ready for Live Tasks**
You may be asked to write Dockerfiles or debug a live container on a shared screen.

---
