# Kubernetes AI Ops Assistant

![GitHub Workflow Status](https://img.shields.io/badge/status-experimental-orange)  
![Python Version](https://img.shields.io/badge/python-3.10+-blue)  
![License](https://img.shields.io/badge/license-MIT-green)

Kubernetes AI Ops Assistant is an AI-powered tool that simplifies Kubernetes cluster management using natural language. It allows DevOps engineers and Kubernetes administrators to monitor, manage, and troubleshoot Kubernetes clusters with the help of Large Language Models (LLMs) and MCP (Model Context Protocol) servers.

---

## 🚀 Features

- **Conversational Cluster Management** – Run Kubernetes operations using plain language commands.  
- **Tool Integration** – Execute commands via specialized MCP servers for Kubernetes and Prometheus.  
- **Deployment Ready** – Dockerized and includes Helm charts for fast deployment.  
- **Interactive Web Interface** – Chainlit-powered chat interface for user-friendly interactions.

---

## 🛠 Prerequisites

- Python 3.10 or higher  
- Docker  
- Access to a Kubernetes cluster  
- Helm for deployment  

---

## ⚡ Local Development Setup

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/kubernetes-ai-ops-agent.git
cd kubernetes-ai-ops-agent

# 2. Install Python dependencies
pip install -r requirements.txt

# 3. Install required MCP servers
npm install -g @kubernetes-ai/mcp-server-kubernetes
pip install prometheus-mcp-server

# 4. Verify Kubernetes config and context
kubectl config view
kubectl config current-context

# 5. Start the Chainlit application
chainlit run src/main.py

##📦 Helm Deployment
# 1. Build and push Docker image
docker build -t myregistry/k8s-ai-ops-agent:latest .
docker push myregistry/k8s-ai-ops-agent:latest

# 2. Create a customized values file
cat <<EOF > customized.values.yaml
image:
  repository: myregistry/k8s-ai-ops-agent

secrets:
  data:
    AZURE_OPENAI_ENDPOINT: "https://my-openai-service.openai.azure.com/"
    AZURE_OPENAI_API_KEY: "my-azure-openai-key"
    AZURE_OPENAI_MODEL: "my-deployment-name"
    OPENAI_API_VERSION: "2023-03-15"

    # Standard OpenAI alternative
    # OPENAI_API_KEY: "my-openai-key"
    # OPENAI_MODEL: "gpt-4o"

    PROMETHEUS_URL: "http://prometheus-service.default:9090"
EOF

# 3. Install Helm chart
cd deploy/helm
helm install kubernetes-ai-ops ./kubernetes-ai-ops-agent -f customized.values.yaml

# 4. Access the web interface locally
kubectl port-forward svc/kubernetes-ai-ops-agent 9000:9000 -n default
