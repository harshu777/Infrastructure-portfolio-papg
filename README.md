# 🏛️ Infrastructure & DevOps Case Study: PAPG Project

> **⚠️ Legal Disclaimer:** This repository serves as a technical portfolio documenting the architecture and DevOps methodologies for a private client project ("PAPG"). Due to Non-Disclosure Agreements (NDA), source code, proprietary configurations, secrets, and client-specific data have been omitted.

---

## 📋 Project At A Glance

| **Role** | **Platform** | **Core Objective** |
| :--- | :--- | :--- |
| **Lead DevOps Engineer** | Kubernetes (On-Prem/Bare Metal) | Architecting a high-availability microservices ecosystem integrating API Gateway, Support Systems, and Headless CMS. |

---

## 🛠️ Technology Stack

### **Orchestration & Infrastructure**
![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)

### **API Management & Traffic**
![Kong](https://img.shields.io/badge/Kong-003459?style=for-the-badge&logo=kong&logoColor=white) ![Traefik](https://img.shields.io/badge/Traefik-24292e?style=for-the-badge&logo=traefik&logoColor=white)

### **Application Services**
![Chatwoot](https://img.shields.io/badge/Chatwoot-46E3B8?style=for-the-badge&logo=chatwoot&logoColor=black) ![Strapi](https://img.shields.io/badge/strapi-%232E7EEA.svg?style=for-the-badge&logo=strapi&logoColor=white) ![Redis](https://img.shields.io/badge/redis-%23DD0031.svg?style=for-the-badge&logo=redis&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)

### **Security & Secrets**
![HashiCorp Vault](https://img.shields.io/badge/Vault-FFFFE3?style=for-the-badge&logo=vault&logoColor=black) ![HashiCorp Consul](https://img.shields.io/badge/Consul-F24C5D?style=for-the-badge&logo=consul&logoColor=white)

---

## 🚀 Architectural Deep Dives

### 1️⃣ Kong API Gateway (Traffic Control Plane)
Deployed **Kong Gateway (v3.x)** as the centralized entry point for all microservices, managing authentication, rate-limiting, and routing.

* **Architecture:**
    * **Ingress Layer:** Traffic enters via Traefik Ingress Controller, which routes to Kong Services.
    * **Admin Security:** The Admin API and Kong Manager UI are exposed via Ingress but protected by strict **IP Whitelisting** annotations (Internal VPNs only).
    * **Database:** Backed by PostgreSQL 9.5 with persistent storage for configuration reliability.



### 2️⃣ Chatwoot (Customer Support Platform)
Deployed a self-hosted instance of **Chatwoot** to manage customer engagement and support tickets.

* **Microservices Orchestration:**
    * Managed the dependency chain ensuring **Redis** and **PostgreSQL** were healthy before the Rails application and Sidekiq workers started.
* **Performance Tuning:**
    * Configured **Horizontal Pod Autoscaling (HPA)** for Sidekiq background workers to handle bursts in incoming messages and email processing.
    * Implemented persistent volume strategies for handling file uploads and attachments.

---

### 3️⃣ Strapi (Headless CMS)
Deployed **Strapi** to serve dynamic content to the frontend application via REST APIs.

* **Custom Build:** Utilized multi-stage Docker builds to package custom plugins and dependencies required by the client.
* **Storage Decoupling:**
    * Separated the database layer (PostgreSQL) from the asset layer (Uploads).
    * Configured a distinct **Persistent Volume Claim (PVC)** for `/public/uploads` to ensure media assets survive container restarts and deployments.

---

### 4️⃣ HashiCorp Ecosystem (Security & Mesh)
Integrated HashiCorp tools to mature the security posture of the cluster.

* **Vault (Secrets Management):**
    * Replaced hardcoded environment variables in Kubernetes manifests.
    * Configured the **Vault Kubernetes Injector** to dynamically inject secrets into pods at runtime, reducing the attack surface.
* **Consul (Service Discovery):**
    * Deployed Consul to map services and manage configuration consistency across the distributed environment.

---

## 🛡️ DevOps & Operational Maturity

### **Secure Configuration Management**
* **Manifests:** All deployments utilize declaritive YAML manifests managed via Git.
* **Secret Injection:** `valueFrom: secretKeyRef` is used universally to abstract sensitive credentials (DB passwords, API keys) from the deployment logic.

### **Disaster Recovery Strategy**
* **StatefulSets:** Utilized for all databases (Postgres, Redis) to ensure stable network identities and ordered rolling updates.
* **Database Migrations:** Automated schema updates using Kubernetes Jobs (e.g., `kong migrations bootstrap`) to ensure "Zero-Touch" upgrades.

---

## 📬 Contact
If you would like to discuss the architectural decisions or Kubernetes strategies demonstrated in this project, feel free to reach out.

[**Your LinkedIn Profile**](https://linkedin.com/in/harshalbaviskar) | [**Your Email**](mailto:hbaviskar777@gmail.com)
