<h1 align="center">🌍 AI Travel Agent</h1>

<p align="center">
  <em>A production-ready AI travel itinerary generator with cloud-native deployment, orchestration, and centralized observability.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white" />
  <img src="https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white" />
  <img src="https://img.shields.io/badge/Groq-F55036?style=for-the-badge&logo=groq&logoColor=white" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
  <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white" />
  <img src="https://img.shields.io/badge/Elasticsearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white" />
  <img src="https://img.shields.io/badge/GCP-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white" />
</p>

---

## 📌 Overview

**AI Travel Agent** is a full-stack AI application that generates personalized day-trip itineraries powered by **LangChain**, **Groq**, and **Llama 3.3 70B**. Beyond the AI core, the project demonstrates a complete **cloud-native DevOps workflow** — from containerization and Kubernetes orchestration to centralized logging with the ELK stack and monitoring via Kibana dashboards.

> This project bridges the gap between AI development and production-ready MLOps/DevOps practices.

---

## 🏗️ Architecture

![AI Travel Agent Architecture](images/AI%20TRAVEL%20AGENT%20Architecture.png)

The project follows a four-stage production workflow:

| Stage | Description |
|---|---|
| **1. Development** | Modular Python app with LangChain chains, a core travel planner, and a Streamlit UI |
| **2. Containerization & Deployment** | Dockerized app with Kubernetes manifests for all services |
| **3. Version Control & Cloud Setup** | GitHub-based source control, GCP VM with Docker, Minikube & Kubectl |
| **4. Build, Deploy & Monitor** | App deployment on Minikube, ELK stack integration, Kibana dashboards |

---

## ✨ Features

- 🤖 **AI-Powered Itinerary Generation** — Uses Llama 3.3 70B via Groq API to generate personalized, interest-based day trip plans
- 🧩 **Modular Architecture** — Clean separation of concerns: config, chains, core logic, and utilities
- 📋 **Structured Logging** — Date-based rotating log files capturing every step of the planning lifecycle
- 🐳 **Dockerized Application** — Reproducible, portable container with a production-grade Streamlit server
- ☸️ **Kubernetes Orchestration** — Full deployment and service manifests for the app and the entire ELK stack
- 📡 **Centralized Observability** — Filebeat → Logstash → Elasticsearch → Kibana pipeline for real-time log monitoring
- ☁️ **GCP Cloud Deployment** — VM-based infrastructure with Minikube for a production-style environment

---

## 🛠️ Tech Stack

| Category | Technologies |
|---|---|
| **Language** | Python 3.10 |
| **AI / LLM** | LangChain, Groq API, Llama 3.3 70B |
| **Frontend** | Streamlit |
| **Containerization** | Docker |
| **Orchestration** | Kubernetes (Minikube) |
| **Logging & Monitoring** | Filebeat, Logstash, Elasticsearch, Kibana (ELK Stack) |
| **Cloud** | Google Cloud Platform (GCP) |
| **Version Control** | GitHub |

---

## 📁 Project Structure

```
AITravelAgent/
├── app.py                    # Streamlit application entry point
├── Dockerfile                # Docker image definition
├── setup.py                  # Package setup and dependency management
├── requirements.txt          # Python dependencies
├── .env                      # Environment variables (Groq API key)
│
├── src/
│   ├── config/
│   │   └── config.py         # API key configuration loader
│   ├── chains/
│   │   └── itinerary_chain.py  # LangChain prompt + Groq LLM chain
│   ├── core/
│   │   └── planner.py        # TravelPlanner class (orchestrates planning flow)
│   └── utils/
│       ├── logger.py         # Date-based rotating file logger
│       └── custom_exception.py  # Structured exception with file/line context
│
├── k8s/
│   ├── k8s-deployment.yaml   # Streamlit app Deployment + LoadBalancer Service
│   ├── filebeat.yaml         # Filebeat DaemonSet + RBAC + ConfigMap
│   ├── logstash.yaml         # Logstash Deployment + ConfigMap + Service
│   ├── elasticsearch.yaml    # Elasticsearch Deployment + PVC + Service
│   └── kibana.yaml           # Kibana Deployment + NodePort Service
│
├── logs/                     # Auto-generated daily log files
└── images/
    └── AI TRAVEL AGENT Architecture.png
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- [Docker](https://docs.docker.com/get-docker/) installed
- [Minikube](https://minikube.sigs.k8s.io/docs/start/) installed (for Kubernetes deployment)
- [kubectl](https://kubernetes.io/docs/tasks/tools/) installed
- A [Groq API key](https://console.groq.com/)

---

### 1. Local Development

**Clone the repository:**

```bash
git clone https://github.com/Anand-Velpuri/AI-TRAVEL-AGENT.git
cd AI-TRAVEL-AGENT
```

**Set up the virtual environment:**

```bash
python -m venv venv
source venv/bin/activate      # On Windows: venv\Scripts\activate
```

**Install dependencies:**

```bash
pip install -e .
```

**Configure environment variables:**

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
```

**Run the Streamlit app:**

```bash
streamlit run app.py
```

Open your browser at `http://localhost:8501`, enter a city and your interests, and click **Generate Itinerary**.

---

### 2. Docker Deployment

**Build the Docker image:**

```bash
docker build -t streamlit-app:latest .
```

**Run the container:**

```bash
docker run -p 8501:8501 --env-file .env streamlit-app:latest
```

The app will be accessible at `http://localhost:8501`.

---

### 3. Kubernetes Deployment (Minikube)

**Start Minikube:**

```bash
minikube start
```

**Load the Docker image into Minikube:**

```bash
minikube image load streamlit-app:latest
```

**Create the Kubernetes secret for the Groq API key:**

```bash
kubectl create secret generic llmops-secrets --from-env-file=.env
```

**Deploy the application:**

```bash
kubectl apply -f k8s/k8s-deployment.yaml
```

**Access the application:**

```bash
minikube service streamlit-service
```

---

### 4. ELK Stack Setup (Logging & Monitoring)

Create the `logging` namespace and deploy all ELK components:

```bash
kubectl create namespace logging

# Deploy in order: Elasticsearch → Logstash → Filebeat → Kibana
kubectl apply -f k8s/elasticsearch.yaml
kubectl apply -f k8s/logstash.yaml
kubectl apply -f k8s/filebeat.yaml
kubectl apply -f k8s/kibana.yaml
```

**Access Kibana dashboard:**

```bash
minikube service kibana -n logging
# Or access directly at: http://<minikube-ip>:30601
```

Once Kibana is running, create an index pattern for `filebeat-*` to start exploring and monitoring logs from all pods.

---

## 🧠 How It Works

```
User Input (City + Interests)
        │
        ▼
  TravelPlanner (src/core/planner.py)
        │   ├── set_city()       → Validates & stores city, appends HumanMessage
        │   ├── set_interests()  → Parses comma-separated interests list
        │   └── create_itinerary() → Calls the LangChain chain
        │
        ▼
  generate_itinerary() (src/chains/itinerary_chain.py)
        │   ├── ChatPromptTemplate → Injects city & interests into system prompt
        │   └── ChatGroq (llama-3.3-70b-versatile, temp=0.3) → Invokes the LLM
        │
        ▼
  Itinerary Text → Displayed in Streamlit UI
        │
        ▼
  Logger → Writes timestamped events to logs/log_YYYY-MM-DD.log
        │
        ▼
  Filebeat → Logstash → Elasticsearch → Kibana (in Kubernetes)
```

---

## 📊 Observability Pipeline

The ELK stack is fully deployed within the Kubernetes `logging` namespace:

| Component | Role | Port |
|---|---|---|
| **Filebeat** | Collects container logs from all nodes via DaemonSet | — |
| **Logstash** | Receives logs from Filebeat on port 5044, forwards to Elasticsearch | 5044 |
| **Elasticsearch** | Indexes and stores all log data with 2Gi persistent storage | 9200 |
| **Kibana** | Visual dashboard for querying and monitoring logs | 5601 / NodePort 30601 |

Filebeat is deployed as a **DaemonSet** with full RBAC permissions to read from `/var/log/containers/` across all nodes, enriching each log event with Kubernetes metadata.

---

## 📝 Logging

The application uses Python's built-in `logging` module with date-based log rotation. Log files are stored in the `logs/` directory and follow the format:

```
logs/log_YYYY-MM-DD.log
```

**Sample log output:**

```
2026-06-20 20:29:19,077 - INFO - Initialized TravelPlanner Instance
2026-06-20 20:29:19,077 - INFO - City set to: Delhi
2026-06-20 20:29:19,078 - INFO - Interests set to: ['Red Fort', 'Lotus Temple', 'Qutub Minar']
2026-06-20 20:29:19,078 - INFO - Generating itinerary for city: Delhi with interests: [...]
2026-06-20 20:29:20,037 - INFO - HTTP Request: POST https://api.groq.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
2026-06-20 20:29:20,059 - INFO - Itinerary generated successfully
```

---

## ⚙️ Environment Variables

| Variable | Description | Required |
|---|---|---|
| `GROQ_API_KEY` | Your Groq API key for LLM access | ✅ Yes |

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add your feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 👤 Author

**Anand Velpuri**

- GitHub: [@Anand-Velpuri](https://github.com/Anand-Velpuri)
- Email: velpurianand8005@gmail.com

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">
  <em>Built with ❤️ — connecting AI development with production DevOps practices.</em>
</p>
