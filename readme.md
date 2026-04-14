# 🔧 Elastic Seamless Provisioning Tool (Elasticsearch 7.9)

This tool automates the provisioning, configuration, and secure setup of an **Elasticsearch 7.9.3 cluster** on **AWS (EC2)** or **GCP (Compute Engine)**.

It uses **Terraform + Ansible** to create infrastructure and configure Elasticsearch and Kibana with security enabled.

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

- Go to your GCP Console: **IAM & Admin → Service Accounts**.
- Create a service account with the **Compute Admin** role.
- Go to the "Keys" tab, click "Add Key", and download the JSON file.
- Export the file path in your terminal so Terraform can find it:

5. Export credentials:

```bash
export GOOGLE_APPLICATION_CREDENTIALS="path/to/service-account.json"
```

6. Verify:

```bash
gcloud auth list
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

After deployment, `Kibana` credentials will be generated.

Access the UI at: https://<KIBANA_NODE_IP>:5601

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

