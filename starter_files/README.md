

# Operationalizing Machine Learning

In this project, we are going to work with the Bank Marketing dataset. The dataset contains information about the marketing campaign of a Portuguese Banking Institute. The classification goal is to predict whether a client will subscribe to a term deposit or not. We use Azure to configure a cloud-based machine learning production model, deploy it, and consume it. Atlast, we will also create, publish, and consume a pipeline.



## Architectural Diagram

![flowchart](https://user-images.githubusercontent.com/55974694/112050855-4cc0b980-8b77-11eb-8071-a35294948b6c.png)



## Key Steps

Key steps involved in this project are:

### 1. Authentication
Using authentication with automation is the best way to go. If authentication is not enabled, human interaction will be required which will interrupt the continuous flow of operations. Hence Continuous Integration and Delivery system (CI/CD) rely on uninterrupted flows. 

Types of Authentication: 1. Key based 2. Token based 3. Interactive


For this experiment the lab which Udacity provided has been used. This step is skipped since this account is not authorized to create a security principal.



### 2. Dataset Registration

The project uses the UCI Bank Marketing Dataset that contains data about banking clients, including personal details of clients like age, job, marital status etc and details regarding maketing campaign. The goal is to predict whether the client will subscribe a term deposit or not, thus making it a binary classification problem with two classes - 'yes' and 'no'.

First, I registered the bank marketing dataset in azure.

A new dataset is created by navigating in datasets section from the left panel of Azure studio. Dataset can be created either by using the web url or by uploading the data from local csv.

![Dataset](https://user-images.githubusercontent.com/55974694/112051909-7b8b5f80-8b78-11eb-95f9-7187b5c6f293.png)


### 3. AutoML Experiment

This feature of Azure allows to build ML models with high scale, efficiency and productivity, all while sustaining model quality. Thus automating the time-consuming, iterative tasks of ML model development.

I ran the AutoML Experiment. The screenshot below shows that the run was completed.

![automl_complete_1](https://user-images.githubusercontent.com/55974694/112052340-0704f080-8b79-11eb-81dc-14371fa3565c.png)


![automl_complete_2](https://user-images.githubusercontent.com/55974694/112052360-0b310e00-8b79-11eb-9824-5bba8c00ecc4.png)


In this step, we will find the best model and use it for our further analysis. Below is the screenshot of our best model.


![Best_Model](https://user-images.githubusercontent.com/55974694/112052754-7d095780-8b79-11eb-9d54-af093a932cec.png)


The best algorithm found is **VotingEnsemble with an accuracy of 91.745%**.



Here's the screenshot of the training parameters of the best model 


![best_model_train_parameters](https://user-images.githubusercontent.com/55974694/112103327-99d07a00-8bcf-11eb-8896-455592feb7da.png)



### 4. Deploy the Best Model

This means shipping the trained model into production, so that it can be consumed by other users as well.


The model is deployed using **Azure Container Instance**.Deploying the best model allows interaction with the HTTP API service and data can be sent over POST requests.

**Deployment triggered**

![Deploying_](https://user-images.githubusercontent.com/55974694/112103409-b40a5800-8bcf-11eb-8036-63b92fb9731b.png)


Once the deployment is transitioned, the state will be shown as Healthy as seen in the screenshot below.


![deployment_state_1](https://user-images.githubusercontent.com/55974694/112103432-bec4ed00-8bcf-11eb-8296-0ef0e65d5a48.png)



![Deployment_state_2](https://user-images.githubusercontent.com/55974694/112103455-ca181880-8bcf-11eb-9228-81fa8d268b04.png)



![Deployment_state_3](https://user-images.githubusercontent.com/55974694/112103442-c5536480-8bcf-11eb-8741-4f26b4a91f8c.png)


**Model deployment succeeded**


![Deployed_](https://user-images.githubusercontent.com/55974694/112103594-ffbd0180-8bcf-11eb-8fcc-06a99a1051c0.png)


### 5. Enable Application Insights


Application Insights is a very useful tool to detect anomalies and visualise performance. It can be enabled before or after deployment and the following information can be collected from the endpoint:

(i)     Output data

(ii)    Responses

(iii)   Request rates, response times and failure rates

(iv)    Dependency rates, response times and failure rates

(v)     Exceptions

### Enabling Application Insights using Python SDK

The logs.py script is used to enable application insights after deployment. The script is run using Azure command line interface.
The statement **service.update(enable_app_insights=True)** enables application insights for the deployment.

The screenshot below is of the logs.py script and logs output, which is the informational output produced by the software, in the form of text.




![logs_1](https://user-images.githubusercontent.com/55974694/112105074-fcc31080-8bd1-11eb-925c-2b3dbe4e0461.png)





![logs_2](https://user-images.githubusercontent.com/55974694/112105062-f765c600-8bd1-11eb-9457-d456d9a1338c.png)




Since the application insights have been enabled, it's shown as true in the properties section.



![application_sights_enabled](https://user-images.githubusercontent.com/55974694/112104980-da30f780-8bd1-11eb-9c07-4b6887ce5672.png)


### 6. Swagger Documentation

Swagger is a tool that helps build, document and consume RESTful web services. It explains what types of HTTP requests that an API can consume like POST and GET.



![deployed_model_swagger_page](https://user-images.githubusercontent.com/55974694/112108227-eb7c0300-8bd5-11eb-8f63-12c06763e237.png)



The HTTP GET is used to retrieve information from a URL.The parameters and responses of the HTTP GET request are as follows:


![GET_1](https://user-images.githubusercontent.com/55974694/112108215-e74fe580-8bd5-11eb-8c77-cf3653f0a574.png)


![GET_2](https://user-images.githubusercontent.com/55974694/112108224-eae36c80-8bd5-11eb-863d-8b8a353701a6.png)




The HTTP POST request is a method used to submit data. The parameters and responses of the HTTP POST request are as follows:



![POST_Parameters_1](https://user-images.githubusercontent.com/55974694/112108231-ecad3000-8bd5-11eb-8361-f998888a2189.png)



![POST_parameters_2](https://user-images.githubusercontent.com/55974694/112108233-ed45c680-8bd5-11eb-8853-9d5ce100bea1.png)



![POST_responses](https://user-images.githubusercontent.com/55974694/112108235-edde5d00-8bd5-11eb-9989-7a4662dc7002.png)


### 7. Consume Model Endpoint

Once a model has been deployed, an endpoint will be available which allows user to send inputs to the trained model and get a response back. This is called  consuming deployed service.HTTP POST is a request method that is used to submit data and HTTP GET is used to retrieve information from a URL. 'endpoint.py' script is used for the same.


![consume_endpoint](https://user-images.githubusercontent.com/55974694/112108238-edde5d00-8bd5-11eb-9925-912706adea0f.png)


### Benchmarking the endpoint

Apache Benchmark is used to load-test the deployed model. It shows a lot of metrics including response time for a deployed model. After configuring the authentication keys, benchmark.sh was run. In this experiment, 10 requests were made where none failed. The average time per request was 159.918 ms.


![Apache_Benchmarking_1](https://user-images.githubusercontent.com/55974694/112109162-39ddd180-8bd7-11eb-8ec6-0eab42b0ae91.png)



![Apache_Benchmarking_2](https://user-images.githubusercontent.com/55974694/112109164-3a766800-8bd7-11eb-951d-2c7edb50ff6a.png)



### 8. Create & Publish pipeline

Pipeline is a great way to automate workflows.


### Creating & Running a pipeline



The Jupyter Notebook provided is run after configuring necessary details.A new pipeline is created with an AutoML step. The pipeline experiment is run and details are displayed using RunDetails widget. 

Here's the screenshot

![rundetails_widget_1](https://user-images.githubusercontent.com/55974694/112109131-2fbbd300-8bd7-11eb-9975-10c0c4f345e8.png)


![rundetails_widget_2](https://user-images.githubusercontent.com/55974694/112109148-34808700-8bd7-11eb-9b3b-5b7113394d7b.png)



### Publishing Pipeline

Publishing a pipeline is the process of making a pipeline publicly available. This can be done both using the SDK and the Studio. When a pipeline is published, a public HTTP endpoint becomes available, allowing other services including external ones to interact with an Azure Pipeline so that they can do work more efficiently.



![published_pipeline_overview_active](https://user-images.githubusercontent.com/55974694/112109156-377b7780-8bd7-11eb-8be1-1bfd510105f0.png)







In this experiment, the pipeline is published using the SDK. Once published, the endpoint details are available and the published pipeline overview can be viewed.





![pipeline_created](https://user-images.githubusercontent.com/55974694/112109159-38aca480-8bd7-11eb-92fe-290de3990314.png)




The pipeline endpoint is marked as Active. Here's the screenshot

 
![pipeline_endpoint](https://user-images.githubusercontent.com/55974694/112109157-38140e00-8bd7-11eb-9071-ed257e1dd00b.png)




## Screen Recording

https://www.youtube.com/watch?v=HtTi4b8sZcU


## Standout Suggestions

1. Apache Benchmark has been used here to load-test the model

2. For future projects, creation of Service Principal can be attempted.

3. We also noticed from the output that the data is biased towards one class. Hence, different sampling methods should be tried.

4. Number of cross-validations can be increased for better results.

5. Using more powerful tools like Deep-learning can definitely lead to better performance.
