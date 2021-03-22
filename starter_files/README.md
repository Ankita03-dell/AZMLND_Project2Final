

# Operationalizing Machine Learning

In this project, we work with the Bank Marketing dataset. The dataset contains information about the marketing campaign of a Portuguese Banking Institute. The classification goal is to predict whether a client will subscribe to a term deposit or not. We use Azure to configure a cloud-based machine learning production model, deploy it, and consume it. Atlast, we will also create, publish, and consume a pipeline.



## Architectural Diagram

![flowchart](https://user-images.githubusercontent.com/55974694/112050855-4cc0b980-8b77-11eb-8071-a35294948b6c.png)



## Key Steps

Key steps involved in this project are:

### Authentication
Using authentication with automation is the best way to go. If authentication is not enabled, human interaction will be required which will interrupt the continuous flow of operations. Hence Continuous Integration and Delivery system (CI/CD) rely on uninterrupted flows. 

Types of Authentication: 1. Key based 2. Token based 3. Interactive

### Dataset registration

First, I registered the bank marketing dataset in azure.


A new dataset is created by navigating in datasets section from the left panel of Azure studio. Dataset can be created either by using the web url or by uploading the data from local csv.

![Dataset](https://user-images.githubusercontent.com/55974694/112051909-7b8b5f80-8b78-11eb-95f9-7187b5c6f293.png)


### AutoML Model

This feature of Azure allows to build ML models with high scale, efficiency and productivity, all while sustaining model quality. Thus automating the time-consuming, iterative tasks of ML model development.

I ran the AutoML Experiment. The screenshot below shows that the run was completed.


*TODO* Remeber to provide screenshots of the `RunDetails` widget as well as a screenshot of the best model trained with it's parameters.

## Screen Recording
*TODO* Provide a link to a screen recording of the project in action. Remember that the screencast should demonstrate:

## Standout Suggestions
*TODO (Optional):* This is where you can provide information about any standout suggestions that you have attempted.
