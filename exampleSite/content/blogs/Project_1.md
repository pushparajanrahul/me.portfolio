---
title: "Predictive Maintenance ML System for Industrial Pumps with Cloud Deployment"
date: 2021-10-15T19:53:33+05:30
draft: false
author: "Rahul Pushparajan"
tags:
  - Python
  - Docker
  - AWS
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
- Temperature (degC)
- Vibration (mm/s)
- FLow Rate (gal/min)

and few output parameters such as :

- Power (kW)
- RPM 

## Dataset

The dataset was created using the below code snippet:

<script src="https://gist.github.com/pushparajanrahul/26cebe5f2ab80d46f532e3209543b14f.js"></script>

   [Built-in Shortcodes](https://gohugo.io/content-management/shortcodes/#use-hugo-s-built-in-shortcodes) for rich content, along with a [Privacy Config](https://gohugo.io/about/hugo-and-gdpr/) and a set of Simple Shortcodes that enable static and no-JS versions of various social media embeds.


The above code generates dataset, measuring the given process variables with 5 min interval for 30days adding some trends and anomalies in the Vibration and introducing a few Temperature changes. 

Also, a few instances of failure event on unfavourable parameter combinations , where the vibration is multiplied by 1.5 times or the temperature has risen 10 degrees beyond the operating range etc.

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

The code snippet is given below:

{{< gist pushparajanrahul f00a30cb589daa5948afb0f0b15d61b1 "train_model.py" >}}

