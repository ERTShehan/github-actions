# GCP Cloud Functions & GitHub Actions

A serverless Python API deployed to **Google Cloud Functions (v2)** using **Terraform**, with a fully automated CI/CD pipeline powered by **GitHub Actions** and secured via **Workload Identity Federation (WIF)**.

## Features

- **Serverless API**: Fetches real-time weather data using the OpenWeatherMap API.
- **Infrastructure as Code (IaC)**: Provisioned on GCP using Terraform (Cloud Functions v2, Cloud Storage, Artifact Registry).
- **Automated CI/CD**: 
  - `pull-request.yml`: Runs tests and Terraform plans on PRs.
  - `deploy.yml`: Deploys the infrastructure and code to GCP upon merging to `main`.
  - `release.yml`: Handles production releases.
- **Enhanced Security**: Keyless authentication to Google Cloud using Workload Identity Federation (OIDC) instead of vulnerable long-lived Service Account JSON keys.

## 🛠️ Technology Stack

- **Language**: Python 3.11 (Functions Framework / Flask)
- **Cloud Provider**: Google Cloud Platform (GCP)
- **IaC Tool**: Terraform 1.7.4
- **CI/CD**: GitHub Actions

## ⚙️ Setup & Deployment

### 1. Prerequisites
- A GCP Project with billing enabled.
- OpenWeatherMap API Key.
- Workload Identity Pool and Provider configured in GCP.

### 2. Environment Variables
Create a `.env` file in the root directory for local testing:
```ini
KEY=your_openweathermap_api_key
```

### 3. Local Development
Run the Makefile to install dependencies and test locally:
```bash
make venv
make run
```

### 4. CI/CD Deployment
Push code to the `main` branch. GitHub Actions will automatically authenticate to GCP using WIF and apply the Terraform configuration to deploy the Cloud Function.

## 🌐 Usage

Once deployed, the API is publicly accessible. Make a GET request with the `city` parameter:
```bash
curl -s "https://[YOUR_CLOUD_FUNCTION_URL]?city=Colombo"
```