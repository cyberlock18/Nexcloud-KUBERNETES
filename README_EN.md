# 🌐 Nextcloud on Kubernetes — ASIR Final Project

> Full deployment of Nextcloud on Ubuntu Server, with security, remote VPN access and evolution towards containers and Kubernetes.

---

## 📋 Table of Contents

1. [Overview](#-overview)
2. [Goals](#-goals)
3. [Architecture](#-architecture)
4. [Networking, security and remote access](#-networking-security-and-remote-access)
5. [Docker and Kubernetes](#-docker-and-kubernetes)
6. [42 Madrid projects on Kubernetes](#-42-madrid-projects-on-kubernetes)
7. [Demos](#-demos)
8. [Documentation](#-documentation)
9. [Author](#-author)

---

## 🔭 Overview

This project is the **Final Year Project (TFG)** of the Higher Technician in Network Computer Systems Administration (ASIR) programme. Its main goal is to deploy **Nextcloud** —a cloud storage and collaboration platform— on **Ubuntu Server**, applying security best practices, automation and high availability.

The environment evolved from a classic bare-metal server installation to an orchestrated deployment with **Kubernetes**, passing through an intermediate stage based on **Docker**. Throughout the process, internal networks (VLAN), secure remote access via VPN, TLS certificates and multiple work zones with role-based access control were configured.

---

## 🎯 Goals

- Deploy Nextcloud securely and accessible from the Internet.
- Set up a custom domain with **TLS/SSL** (Let's Encrypt).
- Protect the server with a **firewall** (UFW) and restricted **SSH** access.
- Provide universal remote access via a **private VPN** (Tailscale).
- Containerise the environment with **Docker** and orchestrate it with **Kubernetes**.
- Use Kubernetes as a platform to spin up instances of **42 Madrid projects**.

---

## 🏗️ Architecture

The system is composed of two servers forming an internal **VLAN** based on containers:

```
Internet
   │
   ▼
[Custom Domain + Let's Encrypt TLS]
   │
   ▼
[Ubuntu Server — Nextcloud]
   ├── Firewall (UFW)
   ├── Restricted SSH
   ├── Tailscale VPN (remote access)
   └── Internal VLAN
         ├── Server 1 (Nextcloud / main services)
         └── Server 2 (workers / replicas)
               ├── Docker → Kubernetes (Minikube / real cluster)
               └── Pods: storage, compilation, metrics
```

The administrator can spin up independent instances to visualise container and system metrics, as well as manage shared file systems accessible by users according to their roles.

---

## 🔒 Networking, security and remote access

| Component | Description |
|---|---|
| **Ubuntu Server** | Base operating system for the server |
| **UFW (Firewall)** | Inbound/outbound rules to minimise the attack surface |
| **SSH** | Secure remote access to the server, with key-based authentication |
| **Custom domain** | DNS pointing to the public server |
| **Let's Encrypt / TLS** | Free SSL certificate with automatic renewal (Certbot) |
| **Tailscale VPN** | Encrypted private network for remote access from anywhere in the world |

The private VPN was a key piece of the project: it allows connecting to the internal environment securely without exposing additional ports on the server.

---

## 🐳 Docker and Kubernetes

The project followed a natural evolution towards containerisation:

1. **Phase 1 — Traditional server**: Nextcloud installed directly on Ubuntu Server.
2. **Phase 2 — Docker**: Services are encapsulated in containers to improve portability and isolation.
3. **Phase 3 — Kubernetes**: Container orchestration to achieve **high availability**, horizontal scaling and declarative management.

Both **Minikube** (local development environment) and a **real multi-node cluster** were evaluated, allowing a comparison of both approaches in terms of performance and operability.

Pods were designed to:
- Run and compile user code.
- Host shared storage services with role-based access control.
- Expose system metrics for administrator monitoring.

---

## 🎓 42 Madrid projects on Kubernetes

Kubernetes was also used as a platform to spin up instances of **42 Madrid cursus projects**, enabling:

- Isolating each project in its own pod/namespace.
- Compiling and running C/C++ code in reproducible environments.
- Managing resources efficiently across multiple simultaneous users.
- Facilitating project submission and evaluation in a standardised environment.

This integration demonstrates the versatility of Kubernetes beyond web hosting, turning it into an educational and development platform.

---

## 🎬 Demos

### Part 1 — Initial setup and deployment

![Demo part 1 — Full setup](./toda_la_parte1-ezgif.com-optimize.gif)

---

### Part 2 — Deployment and containerisation

![Demo part 2 — Docker and Kubernetes](./parte2HechoconClipchamp-ezgif.com-video-to-gif-converter.gif)

---

### Part 3 — Final working system

![Demo part 3 — System in operation](./ezgif.com-video-to-gif-converter.gif)

---

## 📄 Documentation

The following PDF documents contain the full project report:

| Document | Description |
|---|---|
| [📘 Final Project Report (Tailscale v2)](./Memoria_Proyecto_Final_Extendida_Tailscale_v2.pdf) | Extended report covering Tailscale VPN configuration and full deployment |
| [📗 Cloud Server Project — Docker Mix](./PROYECTO_SERVIDOR_EN_LA_NUBE_MIX_DOCKER.pdf) | Documentation of the Docker phase and cloud architecture |

---

## 👤 Author

Project developed as the **ASIR final year project** in the context of technical training and the **42 Madrid** school.

- 🐙 GitHub: [@cyberlock18](https://github.com/cyberlock18)

---

> *"From an Ubuntu server to a Kubernetes cluster — the full journey."*
