## 1. What is Machine Learning?

Machine Learning (ML) is a branch of Artificial Intelligence that enables computers to learn patterns from data or experience and use them to make predictions or decisions without being explicitly programmed with every rule.

Example: An email system learns from examples of spam and legitimate emails to classify incoming messages.

## 2. Supervised Learning

Definition: Supervised learning is a type of ML in which a model learns from labelled data — training examples that contain inputs and their correct answers.

Labelled training data

Email → Spam / Not spam

ML model

Learns input-output patterns

Prediction

New email → Spam

### Two main tasks

A. Classification

Predicts a category or class.

Examples:

- Spam vs not spam
    
- Fraudulent vs legitimate transaction
    
- Cat vs dog image
    

B. Regression

Predicts a numerical value.

Examples:

- House price prediction
    
- Sales forecasting
    
- Estimating temperature
    

### Common supervised learning algorithms

- Linear Regression
    
- Logistic Regression
    
- Decision Tree
    
- Random Forest
    
- Support Vector Machine (SVM)
    
- K-Nearest Neighbors (KNN)
    

Exam keywords: Labelled data, known target, classification, regression.

## 3. Unsupervised Learning

Definition: Unsupervised learning is a type of ML in which a model learns patterns or structures from unlabelled data, without being given the correct output for each training example.

### How it works

Unlabelled data

Customer purchase records without predefined groups

ML model

Discovers patterns or similarities

Discovered groups

Customers with similar buying behavior

### Main tasks

A. Clustering

Groups similar data points together.

Example: A shopping website groups customers into segments based on purchasing behavior.

Common algorithms:

- K-Means
    
- Hierarchical Clustering
    
- DBSCAN
    

B. Dimensionality reduction

Reduces the number of features while retaining useful information.

Example: Simplifying a dataset with hundreds of features to make visualization or analysis easier.

Common technique: Principal Component Analysis (PCA).

C. Association rule learning

Finds items or events that frequently occur together.

Example: Market basket analysis may reveal that customers who buy bread often also buy butter.

Common algorithm: Apriori.

### Applications

- Customer segmentation
    
- Discovering patterns in sales data
    
- Grouping similar documents
    
- Detecting unusual data points
    
- Exploring large datasets
    

Exam keywords: Unlabelled data, hidden patterns, clustering, association.

## 4. Reinforcement Learning

Definition: Reinforcement learning (RL) is a type of ML in which an agent learns by interacting with an environment, receiving rewards or penalties and improving its actions over time.

### How it works

Agent

Chooses an action

Environment

Changes state and returns a reward

Learning

Agent adjusts its future actions to maximize cumulative reward

### Important terms

|Term|Meaning|
|---|---|
|Agent|The learner or decision-maker|
|Environment|The world in which the agent operates|
|State|The current situation|
|Action|A choice made by the agent|
|Reward|Feedback indicating how desirable an outcome is|
|Policy|The strategy used to choose actions|

### Example: Game-playing AI

An agent plays a game:

- It chooses a move.
    
- The game changes state.
    
- It receives a reward or penalty, depending on the reward design.
    
- It learns a strategy that aims to maximize long-term rewards.
    

### Applications

- Game-playing systems
    
- Robotics
    
- Traffic signal optimization
    
- Resource allocation
    
- Autonomous navigation
    

Exam keywords: Agent, environment, actions, rewards, policy.

Note that reinforcement learning does not always require a simple positive or negative reward after every action. Feedback can be delayed, and the objective is generally to maximize cumulative reward.

## 5. Comparison of the three types

|Feature|Supervised|Unsupervised|Reinforcement|
|---|---|---|---|
|Learning signal|Labelled examples|Patterns in unlabelled data|Rewards or penalties|
|Main goal|Predict correct outputs|Discover hidden structure|Learn a reward-maximizing strategy|
|Typical tasks|Classification, regression|Clustering, dimensionality reduction|Sequential decision-making|
|Example|Spam detection|Customer segmentation|Game-playing agent|
|Common algorithms|Linear Regression, Decision Tree, SVM|K-Means, DBSCAN, Apriori|Q-Learning, SARSA|

### Easy memory trick

- Supervised: Learns from examples with answers.
    
- Unsupervised: Finds patterns without given answers.
    
- Reinforcement: Learns through actions and rewards.
### Last-minute revision

1. Supervised: Labelled data → classification or regression.
    
2. Unsupervised: Unlabelled data → clustering or pattern discovery.
    
3. Reinforcement: Agent + environment + actions + rewards → learns a policy.