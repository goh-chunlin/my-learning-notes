# Machine Learning

## What is Machine Learning?
Machine Learning examines **large amount of data** looking for **patterns**, then generates code that lets us **recognize those patterns** in **new data**. Our applications can use the generated code to make better predictions.

Machine Learning applies **statistical techniques** to large amount of data, **looking for the best pattern** to solve our problem. The generated code is referred to as a **Model**, and it can be called by applications that need to solve the problem.

Because Machine Learning helps predict the future, it is often included in the broader category of **Predictive Analytics**.

## Machine Learning Process

Machine Learning process starts with raw data and ends up with a model derived from that data.

## Preparing Data

Getting data in shape for machine learning algorithms to use can be the most consuming part of machine learning project.

## Programming Language for Statistical Programming

Created in New Zealand, the open-source language R has become the lingua franca for writing code in statiscal computing.

## Running Experiements

Once the data is ready, it’s time for the part that most data scientists like best: running experiments. Each experiment runs one or more machine learning algorithms over some part of the prepared data. The result is a model, an implementation of an algorithm that the data scientist hopes will solve the problem at hand, e.g., an algorithm that correctly determines whether a credit card transaction is fraudulent.

An experiment creates a candidate model from prepared data.

## Model Training

In the jargon of machine learning, the process of finding the best model is known as **training the model**.

## Machine Learning Algorithms

Classification Problems: The goal is to create a model that can take a set of input data and accurately determine which of two or more
pre-defined categories this input data falls into.

Regression Problems: Use regression to predict future demand for a product based on previous demand, the weather, and other things. We need historical data about the relationship between demand (the target value) and the other input data (i.e., the features).

Clustering Problems: The goal is find meaningful clusters by examining large amounts of existing input data, then create a model that can figure out from new data about some item what cluster this new item should be assigned to. Azure ML supports only a single
clustering algorithm, called K-Means Clustering, although data scientists can add more if desired.

## Supervised and Unsupervised Learning

Machine learning algorithms can be grouped into two flavors: supervised and unsupervised.

With **Supervised Learning**, you know what target value you're trying to predict. The goal is to map some set of features into the
correct target value for that row. Both classification and regression algorithms are used for supervised learning.

With **Unsupervised Learning**, you don't know what target values you're looking for. Instead, the people running this project have to decide when they're done, i. e. when the model is producing good-enough results. As might be obvious, unsupervised learning problems are generally harder than those using supervised learning. Fortunately, a substantial majority of the most common machine learning scenarios today use supervised learning.

## Testing a Model

Once a candidate model exists for this experiment, the next challenge is to determine how good the model is.

## Deploying and Using a Model

Once the people working on a machine learning project have a model they're happy with, they need a way to deploy that model so it be accessed by applications. A firm in a fast-moving market might need to roll out a new model as often as every week.

To get the right result from a model, the application must provide the right inputs. In other words, the application must provide values for the features that the model needs to determine the correct output. 
