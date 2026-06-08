# End-to-End Deep Learning Project: Chicken Disease Classification

## 📝 Project Overview
This project presents a comprehensive, end-to-end deep learning pipeline focused on chicken disease classification. It utilizes images of chicken feathers to classify whether the chicken is healthy or affected by coccidiosis disease (coxy disease). The primary focus is on implementing best software engineering practices, including modular coding, MLOps integration, and cloud deployment.

## 🛠️ Technologies & Tools
* **Deep Learning Framework:** TensorFlow 2.x Keras API
* **Pre-trained Model:** VGG16 (Transfer Learning)
* **Web Framework:** Flask
* **Pipeline & Data Versioning:** DVC (Data Version Control)
* **CI/CD Automation:** GitHub Actions
* **Containerization:** Docker
* **Cloud Platforms:** AWS (EC2 & ECR) and Azure (ACR & Web App for Containers)

## 🏗️ Project Architecture & Workflow

### 1. Data Ingestion & Setup
* **Data Source:** Downloads a dataset of chicken feather images from GitHub
* **Structure:** Unzips and organizes images into labeled folders (`coxy disease` and `healthy`) stored under `artifacts/data_injection/`
* **Template Setup:** Utilizes an automated Python script (`template.py`) to create a modular, scalable project folder structure, including essential files for logging, utilities, and configurations

### 2. Model Training with Transfer Learning
* **Base Model:** Downloads the pre-trained VGG16 model, freezes its layers, and adds custom dense layers for this specific classification task
* **Callbacks:** Implements TensorFlow callbacks for model checkpointing and TensorBoard logging to monitor training progress
* **Training:** Prepares training/validation data generators and trains the model using defined parameters, saving the output
* **Evaluation:** Evaluates the trained model on validation data, saving quantitative metrics (loss and accuracy) in a JSON format

### 3. MLOps Pipeline with DVC
DVC is integrated to track pipeline stages, cache outputs, and skip re-running unchanged steps to save compute resources

| Stage Number | DVC Stage Name | Key Dependencies | Outputs |
| :--- | :--- | :--- | :--- |
| **01** | `data_injection` | `data_ingestion.py`, `config.yaml` | Downloaded & extracted dataset |
| **02** | `prepare_base_model` | `prepare_base_model.py`, `config.yaml`, `params.yaml` | Base and updated pre-trained models |
| **03** | `model_training` | Training scripts, base model, callbacks | Saved trained model |
| **04** | `model_evaluation` | Trained model, test data | Evaluation metrics JSON |

### 4. Application & UI
* **Flask Web App:** A simple web interface allowing users to upload feather images.
* **Features:** Users can trigger model retraining directly from the UI or get immediate disease classification predictions.

## 🐳 Deployment Strategies
The entire project is containerized using a `Dockerfile` specifying a Python 3.8 image, application dependencies, and AWS CLI tools. 

* **AWS Deployment:** Uses GitHub Actions to build and push the Docker image to AWS Elastic Container Registry (ECR). An EC2 instance configured with a GitHub self-hosted runner pulls and runs the container, exposing port `8080`.
* **Azure Deployment:** Builds and pushes the image to Azure Container Registry (ACR), deploying it on Azure Web App for Containers. Continuous deployment is triggered via GitHub Actions, exposing port `80`.

## 📊 Project Metrics & Parameters
* **Dataset Size:** ~200 images per class (coxy disease vs. healthy)
* **Image Size:** 224 x 224 x 3 (VGG16 input requirement)
* **Batch Size:** 16 (configured in `params.yaml`)
* **Epochs:** 1 (for demo purposes)
* **Docker Image Size:** ~2.5 GB




