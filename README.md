# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
This dataset contains data about marketing campaign information for a bank to get clients to subscribe to a banking deposit. We seek to predict the outcome variable (y) which is the client saying yes to subscribing to a banking deposit. 

The best performing model from the AutoML run was a voting ensamble.  

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**

Setup the training of the data, imported using TabularDatasetFactory, cleaned up teh data. Split the data into train and test data. Used scikit-learn logistic regression model for classification.

Create SKLearn Estimator for the training model, by passing the script and estimator into hyperdrive configuration. 

I used hyperdrive to search for optimal parameters for a logisitc regression. First created a compute cluster using a 'Standard_d2_v2' virtual machine with a maximum of 4 nodes. Then created an early stop policy. 

The parameter sampler used was a random sampling on the inverse of the regularization strength (C) and the maximum iterations (max_iter) as shown in the starter code. It supports discrete and continuous hyperparameters. Supports early termniation of low-performance runs and supports early stopping policies. 

Early Stopping Policy chosen was the BanditPolicy because it is based on slack factor and eval interval. Bandit terminates where the metric is not within the specific slack factor compared to the best perform run. 

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**

For AutoML I imported, cleaned and split the data in the notebook. Then configured the run with time limit and cross validations. I then saved the best resulting model. The Voting Ensamble came out with the best accuracy.

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

Both the approaches follow simlar steps but the differerence is in the configuration. The first approach our ML model is fixed and we use hyperdrive to find optimal hyperparams while in second approach dif models are generated with their own optimal hyperparam values and the best model is then selected. The first approach took around 10 - 15 min and accuracy was around 0.914 and the automl approach took much longer 25 - 30 min and only had a slightly better accuracy around 0.917.

The AutoML results in better accuracy but takes longer to find the better result. It combines multiple ML algorithms so it makes sence that it will find a better result over time.  

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

Measure the fairness of models
Assess which users would be impacted by a specific model and compare multiple models on fairness

## Proof of cluster clean up
Deleted in code

# azure-ml-proj
