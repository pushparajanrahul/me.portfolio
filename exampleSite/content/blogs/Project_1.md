---
title: "Predictive Maintenance ML System for Industrial Pumps with Cloud Deployment"
date: 2024-10-15T19:53:33+05:30
draft: false
author: "Rahul Pushparajan"
tags:
  - Python
  - Feature Engineering
  - RandomForest
  - Docker
  - AWS
  - Streamlit
image: /images/projects/Project1.jpg
description: "An end-to-end ML system that predicts industrial pump failures using sensor data, featuring real-time monitoring through a Streamlit dashboard and robust cloud deployment on AWS"
toc: 
---

In realtime Industrial Automation scenarios, the monitoring and maintenance of assets and field devices for a continuous, smooth and efficient run time is important. 

There are many industrial devices and equipments which have intelligent capabilities and has various measuring parameters that are used to monitor its present operating condition and to calculate its performance on long run.

This project aims in predicting the chances of failure of an Industrial motor, used in various environment such as in water treatment systems, power and utility generation, chemical or pharmaceutical production systems or in petrochemical industries.

## Approach

Here I have created a synthetic dataset considering few input parameters such as :

- Pressure (PSI)
- Temperature (<sup>o</sup>C)
- Vibration (mm/s)
- FLow Rate (gal/min)

and few output parameters such as :

- Power (kW)
- RPM 

## Dataset

The dataset was created using the below code snippet:

<script src="https://gist.github.com/pushparajanrahul/26cebe5f2ab80d46f532e3209543b14f.js"></script>

The above code generates dataset, measuring the given process variables with 5 min interval for 30days adding some trends and anomalies in the Vibration and introducing a few Temperature changes. 

Also, a few instances of failure event on unfavourable parameter combinations , where the vibration is multiplied by 1.5 times or the temperature has risen 10 <sup>o</sup>C beyond the operating range etc.

The obtained dataset is then dumped to a csv as it well be convenient while handling feature engineering in upcoming stage.

## Data Preprocessing


The data, now which is available in csv format is read as a pandas dataframe. Now each process variable is taken in batch of 12, as we have each recording at 5 min interval representing 1 hour in total.

By this, we calculate the rolling mean and rolling standard deviation which is important in indicating gradual deterioration of a steady state.  

We also calculate rate of change of the PV, which might indicate problem/ and abnormality in our use case/ general scenario.

These features are then scaled consistently to treat feature equally while training and predicting in later stages.For this we use the StandardScalar() function from scikit-learn. 

To just brief what the Standard Scalar does:

```commandline

# Consider the example data
original_data = pd.DataFrame({
    'temperature': [100, 150, 200],   # Assuming Temperature holds large values
    'pressure': [0.1, 0.2, 0.3]       # Assuming Pressure holds small values
})

print("Before scaling:")
print(original_data)

scaler = StandardScaler()
scaled = scaler.fit_transform(original_data)
scaled_df = pd.DataFrame(scaled, columns=original_data.columns)

print("\nAfter scaling:")
print(scaled_df)
```


Now, for each feature here, it performs:

z = (x - μ) / σ

where, 

- x = original value
- μ = mean of the feature
- σ = standard deviation
- z = scaled value


And,the output would look like,

```commandline
Before scaling:
   temperature  pressure
0         100       0.1
1         150       0.2
2         200       0.3

After scaling:
   temperature  pressure
0    -1.224745 -1.224745
1     0.000000  0.000000
2     1.224745  1.224745
```

The below code snippet is used for dat preprocessing:

{{< gist pushparajanrahul f00a30cb589daa5948afb0f0b15d61b1 "preprocess.py" >}}

## Training


I have used RandomForest algorithm on which the preprocessed and scaled dataset is trained.

The hyperparameters used here are:
```
- test_size = 0.2 # for train-test split
- n_estimators = 100 # no of decision trees in the forest
```

So, considering a realword scenario, we can say how the voting might happen as below: 

```commandline

# Consider a real-world example

pump_reading = {
    'vibration': 3.2,
    'temperature': 85,
    'pressure': 45,
    'flow_rate': 2.1,
    'power': 75,
    'rpm': 3000
}

Trees voting process:
Tree 1: Checks vibration + temperature → Predicts Failure
Tree 2: Checks pressure + flow_rate → Predicts Failure
Tree 3: Checks rpm + power → Predicts Normal
```
*Note: I will be soon writing few blog articles on each AI algorithms and will tag along to refresh the concepts.*

The code snippet is given below:

{{< gist pushparajanrahul f00a30cb589daa5948afb0f0b15d61b1 "train_model.py" >}}

The model is finally saved using Joblib function as pickel file to be used later in our dashboard/ production environment.


## Dashboard using Streamlit

Streamlit is very simple to learn and for a beginner it still may take some time. I had few assistance of the official streamlit documentation and ClaudeAI to help me complete just the dashboard part at the time of building it.

The interactive display windows are given below:

