---
layout: page
title: MLOps Project for Online Learning
# description: with background image
img: assets/img/projects/ybigta_onn/mlops_pipeline.png
importance: 1
category: work
related_publications: false
---


<!-- To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    --- -->

## About
InfantinO is an online learning framework targeting infants' facial expression classification which provides management about unconventional machine learning lifecycle including annotation & model update. Label ambiguity, catastrophic forgetting under frequent domain shift, insufficient dataset is a main challenge of infants' facial expression classification. These challenges can be overcome with our framework, which utilizes domain adaptation & online learning


## Project Procedure

  (1) Collect infant face expression data
  - Facial expression to 7 categories : {angry, disgust, fear, happy, sad, surprise, neutral}
  - Collect Dataset through google
  - Image augmentation
  
  (2) Train Feature Extractor
  - Using timm, create 'efficientnet-b0' model with 64 output layers
  - Add classifying layer with 7 outputs
  - Train the model with infant data
  - Extract only feature extration structure and weights of the model
  - Connect the Feature Extactor with scikitlearn MLP Classifier

  (3) Conduct Online learning through MLFlow
  - Using MLFlow, train the model with Online Learning method
  - Online Learning enables superfast re-training without catastrophic forgetting


## MLops

<p align="center"><img src = "/assets/img/projects/ybigta_onn/Untitled.png" width="60%" height="60%"></p>

We developed the MLops pipeline for this project mainly using ‘mlflow’, ‘Azure Machine Learning’, and aws services.

In this picture, MLops cycle goes counter-clockwise starting from the bottom-right.

The cycle consists of 3 parts: Model training, Model deploying, and Model retraining. 

### Ⅰ. Model Training

1. Train model

- Train ONN model with infant data
- Track the model training with MLflow
    - MLflow is a platform to manage an ML lifecycle. MLflow lets us log source properties, parameters, metrics, and artifacts related to training an ML model.
- Save an MLflow artifact in an S3 bucket
    
    If we train the model with MLflow, we can record MLflow entities(runs, parameters, metrics, metadata, etc.) to various remote file storage solutions. 
    
    We chose S3 Bucket for storage.
    
2. Fetch a model information and register to Azure Model Registry
    - [Model registration](https://learn.microsoft.com/en-us/azure/machine-learning/concept-model-management-and-deployment) allows you to store and version your models in the Azure cloud, in your workspace. The model registry helps you organize and keep track of your trained models.
    - Get the ‘.pkl’ file of the model from the S3 bucket
    - Register the ‘.pkl’ file to AzureML Model Registry by naming the model with the model version
        
<p align="center"><img src = "/assets/img/projects/ybigta_onn/Untitled 1.png" width="40%" height="40%"></p>

        
<p align="center"><img src = "/assets/img/projects/ybigta_onn/Untitled 2.png" width="40%" height="40%"></p>

        
### Ⅱ. Model Deploying

#### 1. Create an environment 
- In AzureML, you can define an environment from a Docker image, a Docker build context, and a conda specification with a Docker image. Azure ML Environments are used to define the containers where your code will run.
- We made an environment starting from the existing environment. The environment is uploaded to ACR.

<p align="center"><img src = "/assets/img/projects/ybigta_onn/Untitled 3.png" width="40%" height="40%"></p> 
- Customize the environment by editing the DockerFile. We added some required packages.
                
<p align="center"><img src = "/assets/img/projects/ybigta_onn/Untitled 5.png" width="40%" height="40%"></p>

        
        
#### 2. Create an endpoint
- Use Azure Machine Learning endpoints to streamline model deployments for both real-time and batch inference deployments. Endpoints provide a unified interface to invoke and manage model deployments across compute types. An endpoint, in this context, is an HTTPS path that provides an interface for clients to send requests (input data) and receive the inferencing (scoring) output of a trained model.
- To create an online endpoint in AzureML, we need to specify four elements
  - (a) Model files or a registered model in the workspace
    - Here we used the model registered in Model Registry above. We need to choose a model version by considering the accuracy of the models.
    
    <p align="center"><img src = "/assets/img/projects/Untitled 6.png" width="40%" height="40%"></p>
  - (b) Scoring script
    - The scoring script is a Python file (`.py`) that contains the logic about how to run the model and read the input data submitted by the batch deployment executor driver.
    
    <p align="center"><img src = "/assets/img/projects/ybigta_onn/Untitled 7.png" width="40%" height="40%"></p>
  - (c) Environment
  
  <p align="center"><img src = "/assets/img/projects/ybigta_onn/Untitled 8.png" width="40%" height="40%"></p>
  - (d) Computing instance, scale setting
  
  <p align="center"><img src = "/assets/img/projects/ybigta_onn/Untitled 9.png" width="40%" height="40%"></p>        
    

#### Users can make 2 actions on our website.

A. Make an inference request of one baby picture.

B. Upload a pair of baby-picture and label to retrain the model. 

Action A.

1. Node.js server gets an image and stores it in the s3 bucket.
2. Node.js server sends the s3 bucket URI of the image to the AzureML endpoint.
3. AzureML endpoint returns the inference result.

### Ⅲ. Model Retraining

Action B.

1. Node.js server stores the pair of information in the s3 bucket.
2. In the local environment, keep track of the number of data in the s3 bucket. And if the number of data increases, retrains the model with the most recently stored data.
 

## Presentation Slides
<div class="row">
    <div class="col-sm-12 mt-3 mt-md-0">
        <div class="embed-responsive embed-responsive-16by9">
            <iframe class="embed-responsive-item" src="https://drive.google.com/file/d/1jGR_O3MjBp1_BM5LIkHuCcIx1niGuEpg/preview" allow="autoplay"></iframe>
        </div>
    </div>
</div>