# An end to end demo on MLOps on SageMaker

### Prerequisites
The following prerequisites must be completed to replicate this project.

From the SageMaker Studio UI, create a SageMaker Project using one of the 1st party supported templates. Please use one of the following templates - 
* *MLOps template for model building, training, and deployment*
* *MLOps template for model building, training, and deployment with third-party Git repositories using Jenkins*
* *MLOps template for model building, training, and deployment with third-party Git repositories using CodePipeline*

*Note - It is recommended to use the first template which leverages SageMaker native services for Source Version Control and CI/CD. This reduces the number of steps needed for an end to end demo. If choosing the other templates, please follow the documentation to complete the template specific prerequisites. 

For more information on SageMaker Projects, visit the AWS [documentation](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-projects-whatis.html). 

Once the project is created, you will see 2 repositories created - one for the model building code and one for the model deployment code. The model deployment code will remain untouched, the model building code will be changed by replacing `pipelines/abalone/` with the code from this repo under `sagemaker-pipeline/`

### Repository Structure

This repository contains 2 folders -
* `sagemaker-pipeline/`
    This folder contains a code to create and run a SageMaker Pipeline to process data, run a hyperparameter tuning job, evaluate the top model from the HPO job, use Clarify to generate a bias report, and register the model into a model registry. 
* `model-monitor`
    This folder contains notebooks for creating an endpoint from a model registered in the model registry and setting up a Data Quality Monitor. 

### Demo Setup

* Navigate to the model build repo created by the SageMaker Project, replace the code in `pipelines/abalone/` with the code in `sagemaker-pipeline/`. 
* Trigger the pipeline by pushing the new code to the CodeCommit/Git repo (depending on the template selected)
* Once the pipeline has completed, find the model package group in the Model Registry and find the ARN of the model package created in the group
* Approve the model in the model registry, this will trigger the model deployment pipeline, you should see an endpoint being created in SageMaker

Setup Model Monitor
* Navigate to `model-monitor/create_endpoint.ipynb` to create an endpoint with DataCapture enabled
* Run `model-monitor/data_quality_monitor.ipynb` to set up a Data Quality Monitoring schedule on the endpoint. 


