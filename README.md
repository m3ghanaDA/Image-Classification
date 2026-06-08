# End-to-End Deep Learning Project: Chicken Disease Classification

## 📝 Project Overview
This project presents a comprehensive, end-to-end deep learning pipeline focused on chicken disease classification[cite: 1]. It utilizes images of chicken feathers to classify whether the chicken is healthy or affected by coccidiosis disease (coxy disease)[cite: 1]. The primary focus is on implementing best software engineering practices, including modular coding, MLOps integration, and cloud deployment[cite: 1].

## 🛠️ Technologies & Tools
* **Deep Learning Framework:** TensorFlow 2.x Keras API[cite: 1]
* **Pre-trained Model:** VGG16 (Transfer Learning)[cite: 1]
* **Web Framework:** Flask[cite: 1]
* **Pipeline & Data Versioning:** DVC (Data Version Control)[cite: 1]
* **CI/CD Automation:** GitHub Actions[cite: 1]
* **Containerization:** Docker[cite: 1]
* **Cloud Platforms:** AWS (EC2 & ECR) and Azure (ACR & Web App for Containers)[cite: 1]

## 🏗️ Project Architecture & Workflow

### 1. Data Ingestion & Setup
* **Data Source:** Downloads a dataset of chicken feather images from GitHub[cite: 1].
* **Structure:** Unzips and organizes images into labeled folders (`coxy disease` and `healthy`) stored under `artifacts/data_injection/`[cite: 1].
* **Template Setup:** Utilizes an automated Python script (`template.py`) to create a modular, scalable project folder structure, including essential files for logging, utilities, and configurations[cite: 1].

### 2. Model Training with Transfer Learning
* **Base Model:** Downloads the pre-trained VGG16 model, freezes its layers, and adds custom dense layers for this specific classification task[cite: 1].
* **Callbacks:** Implements TensorFlow callbacks for model checkpointing and TensorBoard logging to monitor training progress[cite: 1].
* **Training:** Prepares training/validation data generators and trains the model using defined parameters, saving the output[cite: 1].
* **Evaluation:** Evaluates the trained model on validation data, saving quantitative metrics (loss and accuracy) in a JSON format[cite: 1].

### 3. MLOps Pipeline with DVC
DVC is integrated to track pipeline stages, cache outputs, and skip re-running unchanged steps to save compute resources[cite: 1].

| Stage Number | DVC Stage Name | Key Dependencies | Outputs |
| :--- | :--- | :--- | :--- |
| **01** | `data_injection` | `data_ingestion.py`, `config.yaml` | Downloaded & extracted dataset[cite: 1] |
| **02** | `prepare_base_model` | `prepare_base_model.py`, `config.yaml`, `params.yaml` | Base and updated pre-trained models[cite: 1] |
| **03** | `model_training` | Training scripts, base model, callbacks | Saved trained model[cite: 1] |
| **04** | `model_evaluation` | Trained model, test data | Evaluation metrics JSON[cite: 1] |

### 4. Application & UI
* **Flask Web App:** A simple web interface allowing users to upload feather images[cite: 1].
* **Features:** Users can trigger model retraining directly from the UI or get immediate disease classification predictions[cite: 1].

## 🐳 Deployment Strategies
The entire project is containerized using a `Dockerfile` specifying a Python 3.8 image, application dependencies, and AWS CLI tools[cite: 1]. 

* **AWS Deployment:** Uses GitHub Actions to build and push the Docker image to AWS Elastic Container Registry (ECR)[cite: 1]. An EC2 instance configured with a GitHub self-hosted runner pulls and runs the container, exposing port `8080`[cite: 1].
* **Azure Deployment:** Builds and pushes the image to Azure Container Registry (ACR), deploying it on Azure Web App for Containers[cite: 1]. Continuous deployment is triggered via GitHub Actions, exposing port `80`[cite: 1].

## 📊 Project Metrics & Parameters
* **Dataset Size:** ~200 images per class (coxy disease vs. healthy)[cite: 1]
* **Image Size:** 224 x 224 x 3 (VGG16 input requirement)[cite: 1]
* **Batch Size:** 16 (configured in `params.yaml`)[cite: 1]
* **Epochs:** 1 (for demo purposes)[cite: 1]
* **Docker Image Size:** ~2.5 GB[cite: 1]

## Workflows

1. Update config.yaml
2. Update secrets.yaml [Optional]
3. Update params.yaml
4. Update the entity
5. Update the configuration manager in src config
6. Update the components
7. Update the pipeline 
8. Update the main.py
9. Update the dvc.yaml


# How to run?
### STEPS:

Clone the repository

```bash
https://github.com/m3ghanaDA/Chicken-Disease-Classification
```
### STEP 01- Create a conda environment after opening the repository

```bash
conda create -n cnncls python=3.8 -y
```

```bash
conda activate cnncls
```


### STEP 02- install the requirements
```bash
pip install -r requirements.txt
```


```bash
# Finally run the following command
python app.py
```

Now,
```bash
open up you local host and port
```


### DVC cmd

1. dvc init
2. dvc repro
3. dvc dag



# AWS-CICD-Deployment-with-Github-Actions

## 1. Login to AWS console.

## 2. Create IAM user for deployment

	#with specific access

	1. EC2 access : It is virtual machine

	2. ECR: Elastic Container registry to save your docker image in aws


	#Description: About the deployment

	1. Build docker image of the source code

	2. Push your docker image to ECR

	3. Launch Your EC2 

	4. Pull Your image from ECR in EC2

	5. Lauch your docker image in EC2

	#Policy:

	1. AmazonEC2ContainerRegistryFullAccess

	2. AmazonEC2FullAccess

	
## 3. Create ECR repo to store/save docker image
    - Save the URI: 637423243273.dkr.ecr.eu-north-1.amazonaws.com/chicken
    

	
## 4. Create EC2 machine (Ubuntu) 

## 5. Open EC2 and Install docker in EC2 Machine:
	
	
	#optinal

	sudo apt-get update -y

	sudo apt-get upgrade
	
	#required

	curl -fsSL https://get.docker.com -o get-docker.sh

	sudo sh get-docker.sh

	sudo usermod -aG docker ubuntu

	newgrp docker
	
# 6. Configure EC2 as self-hosted runner:
    setting>actions>runner>new self hosted runner> choose os> then run command one by one


# 7. Setup github secrets:

    AWS_ACCESS_KEY_ID=

    AWS_SECRET_ACCESS_KEY=

    AWS_REGION = us-east-1

    AWS_ECR_LOGIN_URI = demo>>  566373416292.dkr.ecr.ap-south-1.amazonaws.com

    ECR_REPOSITORY_NAME = simple-app




# AZURE-CICD-Deployment-with-Github-Actions

## Save pass:

s3cEZKH5yytiVnJ3h+eI3qhhzf9q1vNwEi6+q+WGdd+ACRCZ7JD6


## Run from terminal:

docker build -t chickenapp.azurecr.io/chicken:latest .

docker login chickenapp.azurecr.io

docker push chickenapp.azurecr.io/chicken:latest


## Deployment Steps:

1. Build the Docker image of the Source Code
2. Push the Docker image to Container Registry
3. Launch the Web App Server in Azure 
4. Pull the Docker image from the container registry to Web App server and run 
