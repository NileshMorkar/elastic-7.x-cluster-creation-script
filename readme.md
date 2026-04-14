# 🔧 Elastic Seamless Provisioning Tool (Elasticsearch 7.9)

This tool automates the provisioning, configuration, and secure setup of an **Elasticsearch 7.9.3 cluster** on **AWS (EC2)** or **GCP (Compute Engine)**.

It uses **Terraform + Ansible** to create infrastructure and configure Elasticsearch and Kibana with security enabled.

---

## 🚀 What This Tool Does

- Creates a full Elasticsearch 7.9 cluster (Master, Data, Ingest nodes)
- Deploys infrastructure on AWS or GCP
- Installs and configures Elasticsearch + Kibana
- Enables **basic authentication**
- Generates **internal TLS certificates (.p12)**
- Automatically builds dynamic Ansible inventory

---

## 🧰 Tech Stack

- Terraform → Infrastructure provisioning
- Ansible → Configuration management
- Python → Orchestration scripts

---

## 📋 Prerequisites

Make sure these are installed on your system:

- Terraform ≥ 1.x
- Python 3.x
- Ansible
- pip

---

## ☁️ Cloud Setup (IMPORTANT)

You must configure cloud credentials before running the script.

---

### 🔵 AWS Setup

1. Install AWS CLI
2. Run:

```bash
aws configure
```

3. Enter:

- AWS Access Key
- AWS Secret Key
- Default region (e.g., ap-south-1)

4. Verify:

```bash
aws sts get-caller-identity
```

---

### 🔴 GCP Setup

1. Install Google Cloud SDK
   https://cloud.google.com/sdk/docs/install

2. Authenticate:

```bash
gcloud auth login
```

3. Set project:

```bash
gcloud config set project <PROJECT_ID>
```

4. Create service account (if not already):

- Go to IAM → Service Accounts
- Create key → JSON

5. Export credentials:

```bash
export GOOGLE_APPLICATION_CREDENTIALS="path/to/service-account.json"
```

6. Verify:

```bash
gcloud auth list
```

---

## ⚙️ Configuration

Before running the script, update configuration files:

### 1. Terraform Variables

Update:

```
terraform/variables.tf
```

Important fields:

- region
- instance_type
- node_count
- cloud_provider (aws/gcp)

---

### 2. Cluster Configuration

Update:

```
config/cluster_config.yaml
```

Example:

```yaml
cluster_name: elastic-cluster
master_nodes: 1
data_nodes: 1
ingest_nodes: 1
```

---

## 🖥️ Local Setup

### 1. Create Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

---

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 🚀 Create Cluster

```bash
python main.py
```

This will:

1. Provision infrastructure using Terraform
2. Generate Ansible inventory
3. Configure Elasticsearch & Kibana

---

## 🔐 IMP: Credentials

After deployment, `Kibana` credentials will be generated:

- Username: `hyperflex`
- Password: Elastic@123

---

## 🧹 Destroy Cluster

```bash
python destroy.py
```

---

## ⚠️ Notes

- Make sure ports **9200** and **5601** are accessible
- Ensure your IP is allowed in cloud firewall/security group
- Default version: **Elasticsearch 7.9.3**

---

## ❓ Troubleshooting

### Terraform Issues

```bash
terraform init
terraform apply
```

---

### Ansible Issues

```bash
ansible --version
```

---

### Permission Issues

- AWS → Check IAM permissions
- GCP → Check service account roles

---

