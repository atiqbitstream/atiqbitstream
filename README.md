<div align="center">

# Atiq Ur Rehman

### I build real-time systems end to end: the mobile client, the event-driven backend, and the cloud beneath them.

[![GitHub](https://img.shields.io/badge/GitHub-atiqbitstream-181717?style=flat-square&logo=github)](https://github.com/atiqbitstream)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Atiq_Ur_Rehman-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/atiq-ur-rehman-28976333a)
[![Email](https://img.shields.io/badge/Email-mukroatiq%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:mukroatiq@gmail.com)
[![YouTube](https://img.shields.io/badge/YouTube-Channel-FF0000?style=flat-square&logo=youtube&logoColor=white)](https://www.youtube.com/@atiqkhan-e3h)

</div>

I build software that has to run in real time and hold up under load. Over the last two and a half years I have carried systems the whole distance, from a Bluetooth packet leaving a device to an autoscaling service on AWS: a React Native client, a set of FastAPI microservices communicating over Kafka, the signal processing that runs between them, and the Terraform that provisions all of it. Most recently I led the engineering for Niura, a neurotech company building EEG earbuds, where I was the sole or majority author of a real-time brain-signal platform across three product generations.

I care about the parts that are easy to get wrong: backpressure, concurrency, data isolation, and the difference between a system that demos well and one that survives twenty users at once.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white)
![React Native](https://img.shields.io/badge/React_Native-61DAFB?style=flat-square&logo=react&logoColor=black)
![Apache Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)

Open to full-stack and full-stack AI engineering roles, remote, hybrid, or with relocation.

## Featured work

### Niura, real-time EEG earbud platform

A neuro-productivity platform that turns live brain signals into useful insight. Two EEG earbuds each emit about 255 samples per second over Bluetooth LE. A React Native app decodes the packets, synchronizes the left and right channels by sample index, and streams them over authenticated WebSockets into a five-service FastAPI backend. Apache Kafka carries the high-frequency data between services, an EEG service runs SciPy and BrainFlow FFT band-power analysis on isolated Celery workers to compute focus, stress, and wellness, and the results stream back to the app in real time. I also designed an AI assistant that converts voice and images into EEG-aware calendar schedules. The full environment is provisioned on AWS with modular Terraform, including ECS Fargate, RDS, ElastiCache, MSK Serverless Kafka, S3, Lambda, and a VPC with a bastion host, and is observed through Grafana, Loki, and Prometheus.

I was the sole or majority author across every repository, confirmed by git history, including roughly 260 of 268 commits on the most recent "Zone" rebuild. The product is live at [niura.io](https://www.niura.io/). The code lives in the company's private repositories.

**Stack:** React Native, Expo, FastAPI, Apache Kafka, Celery, Redis, SciPy, BrainFlow, PostgreSQL, TimescaleDB, AWS, Terraform, Docker.

### The hard part: twenty devices, one deadlock, fixed under live pressure

Niura ran a live on-site demo with Audi in which about twenty paired earbuds and phones streamed EEG at the same time. Under that concurrency the database deadlocked and the backend stalled. The obvious suspect was the database, and I first reached for TimescaleDB, but the real cause was the request pattern: every client was opening fresh HTTP connections every couple of seconds. I moved bulk ingestion to a process pool with a fresh database session per worker, isolated each device into its own per-event TimescaleDB hypertables, tuned the connection pool with READ COMMITTED isolation and fail-fast timeouts plus live pool monitoring, and replaced the heavy real-time database path with a lightweight band-FFT streamed over WebSockets. The demo held. The lesson stuck: profile the request pattern before you blame the database.

### MoveToYou, multi-tenant delivery platform

A full delivery-management system that serves several dairy businesses from a single instance. The backend is a NestJS and TypeORM service with row-level tenant isolation scoped by organization, role-based access control for admin, user, and rider, and more than thirty-five validated endpoints over a ten-entity relational domain. The web client is a server-side-rendered Angular application with role-aware navigation, JWT interceptors, and drag-and-drop route reordering. Authentication runs as a separate NestJS identity service that issues database-backed JWT sessions with single-active-session enforcement and server-side revocation, so a token can be invalidated the moment a role changes.

**Stack:** NestJS, TypeORM, PostgreSQL, Angular (SSR), Angular Material, RxJS, Tailwind CSS, JWT.
[Backend](https://github.com/atiqbitstream/movetoyou-backend) · [Frontend](https://github.com/atiqbitstream/movetoyou-frontend) · [Auth service](https://github.com/atiqbitstream/secnotify-auth-backend)

### Selected projects

| Project | What it is | Stack |
|---------|------------|-------|
| [womb-backend](https://github.com/atiqbitstream/womb-backend) | A FastAPI and PostgreSQL backend for a biofeedback wellness platform: IoT therapy-device control, multi-domain health monitoring, an admin approval workflow, and a CMS, across 80+ JWT-secured endpoints. | FastAPI, SQLAlchemy, PostgreSQL, JWT |
| [mca-lender-detection-api](https://github.com/atiqbitstream/mca-lender-detection-api) | An NLP pipeline for a fintech client that flags merchant-cash-advance lender payments in messy bank-transaction text using sentence-transformer embeddings and cosine similarity, with a confidence-threshold review path. | Python, sentence-transformers, scikit-learn |
| [IntelliBank-Kafka](https://github.com/atiqbitstream/IntelliBank-Kafka) | Event-driven banking microservices that communicate only over Apache Kafka, containerized and deployed to IBM Cloud Code Engine through a GitHub Actions pipeline. | NestJS, Apache Kafka, Docker, IBM Cloud |
| [ibm-ecommerce-infra](https://github.com/atiqbitstream/ibm-ecommerce-infra) | Terraform infrastructure as code provisioning a load-balanced, autoscaling VPC web tier and a managed PostgreSQL database on IBM Cloud. | Terraform, IBM Cloud |
| [boloprompt](https://github.com/atiqbitstream/boloprompt) | An offline macOS menu-bar app for long-form voice dictation that transcribes locally on Apple Silicon with Whisper. | Swift, WhisperKit |

## What I work with

| Area | Tools |
|------|-------|
| Languages | Python, TypeScript, JavaScript, SQL |
| Backend | FastAPI, NestJS, Node.js, REST, WebSockets, Celery, Passport and JWT |
| Frontend and mobile | React Native, Expo, Angular with SSR, React and Next.js, RxJS, Tailwind CSS, Bluetooth LE |
| Data, signal, and ML | NumPy, SciPy, BrainFlow, pandas, sentence-transformers, scikit-learn, OpenAI API |
| Streaming and messaging | Apache Kafka, Redis |
| Databases | PostgreSQL, TimescaleDB, TypeORM, SQLAlchemy, Redis |
| Cloud and DevOps | AWS (ECS, RDS, MSK, Lambda, S3, VPC), Terraform, Docker, IBM Cloud, GitHub Actions, Grafana, Loki, Prometheus, k6 |
| Architecture | Event-driven microservices, real-time streaming, multi-tenant data isolation, RBAC, stateful JWT auth |

## Education

**BS in Computer Science**, specialization in Artificial Intelligence
COMSATS University Islamabad, Wah Campus, 2021 to 2024.

## Connect

Based in Pakistan, open to remote work and relocation.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/atiq-ur-rehman-28976333a)
[![Email](https://img.shields.io/badge/Email-mukroatiq%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:mukroatiq@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-atiqbitstream-181717?style=flat-square&logo=github)](https://github.com/atiqbitstream)
