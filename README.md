## Building a Scalable Personalized Healthcare Recommendation System using Python & Big Data Pipelines
### Data set: 
Blood transfusion saves lives - from replacing lost blood during major surgery or a serious injury to treating various illnesses and blood disorders. Ensuring that there's enough blood in supply whenever needed is a serious challenge for the health professionals. According to WebMD, "about 5 million Americans need a blood transfusion every year".

Our dataset is from a mobile blood donation vehicle in Taiwan. The Blood Transfusion Service Center drives to different universities and collects blood as part of a blood drive. We want to predict whether or not a donor will give blood the next time the vehicle comes to campus. The data is stored in datasets/transfusion.data and it is structured according to RFMTC marketing model (a variation of RFM).

**Dataset Overview**  

- **Total Rows**: 748  
- **Total Columns**: 5  
- **Data Type**: Pure numeric  

Here is the information presented in a table format:

| Column     | Description (Inferred)                                   | Type   |
|------------|---------------------------------------------------------|--------|
| Recency    | How recently a person donated (in months)               | int64  |
| Frequency  | Total number of donations                                | int64  |
| Monetary   | Total blood donated (c.c.)                              | int64  |
| Time       | Time since first donation (in months)                   | int64  |
| Class      | Target: 1 indicates they might donate again; 0 indicates they might not | int64  |


This dataset consists of 748 entries, each represented by 5 numeric features, which will be used to train our reinforcement learning agent for donor engagement.

### Objective

Design and deploy a system that processes patient bloodwork data to generate personalized health insights and lifestyle recommendations using data engineering workflows and lightweight ML models.

### Reinforcement Learning Pipeline for Donor Engagement

#### Objective:
Train a Reinforcement Learning (RL) agent to make decisions regarding donor engagement, specifically:
1. Whether to contact a donor.
2. What type of message or incentive to use.

#### Setup

- **Environment**: The environment is based on a dataset that includes the following features:
  - **Recency**: How recently the donor has interacted.
  - **Frequency**: How often the donor has interacted.
  - **Monetary**: The total amount donated by the donor.
  - **Time**: The time since the donor's last interaction.
  - **Class**: The classification of the donor (e.g., high-value, low-value).

- **State**: The state is represented as a vector of the four features mentioned above:
  \[
  \text{State} = [\text{Recency}, \text{Frequency}, \text{Monetary}, \text{Time}]
  \]

- **Action Space**: The agent has the following actions it can take:
  - **0**: Do nothing
  - **1**: Send SMS
  - **2**: Send Email
  - **3**: Offer incentive

- **Reward Function**: The reward function is designed to encourage positive donor responses and penalize wasteful messages. For example:
  - Reward more when donors respond positively after being nudged (e.g., making a donation).
  - Penalize for sending messages that do not result in a positive response or lead to donor disengagement.

#### Tools Used:
1. **gymnasium & OpenAI Gym**: These libraries can be used to simulate the donor environment, allowing the agent to interact with the environment and learn from it.
2. **stable-baselines3**: This library provides implementations of various RL algorithms, such as Proximal Policy Optimization (PPO) or Deep Q-Networks (DQN), which can be used to train the agent.
3. **ray[rllib]** (optional): This library can be used for scaling experiments, allowing for distributed training and evaluation of the RL agent.

<img width="2846" height="1518" alt="image" src="https://github.com/user-attachments/assets/3271534a-3f1e-471b-b8f4-18330bb525f0" />
