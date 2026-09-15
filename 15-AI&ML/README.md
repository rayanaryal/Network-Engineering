# AI & Machine Learning

Artificial Intelligence (AI) and Machine Learning (ML) are becoming increasingly important in modern networking. Network platforms can use AI and ML to analyse network behaviour, identify anomalies, predict problems, classify endpoints, optimise wireless networks, and assist network engineers with troubleshooting and configuration.

This section documents my understanding of **Artificial Intelligence, Machine Learning, Deep Learning, Predictive AI, Generative AI**, and their applications in modern network environments, including **Cisco Catalyst Center**.

---

# Table of Contents

- [What is AI?](#what-is-ai)
- [What is ML?](#what-is-ml)
- [AI vs ML](#ai-vs-ml)
- [Types of Machine Learning](#types-of-machine-learning)
  - [Supervised Learning](#supervised-learning)
  - [Unsupervised Learning](#unsupervised-learning)
  - [Reinforcement Learning](#reinforcement-learning)
  - [Deep Learning](#deep-learning)
- [Predictive and Generative AI](#predictive-and-generative-ai)
  - [Predictive AI](#predictive-ai)
  - [Generative AI](#generative-ai)
  - [AI Hallucinations](#ai-hallucinations)
- [Predictive and Generative AI in Networks](#predictive-and-generative-ai-in-networks)
- [AI in Cisco Catalyst Center](#ai-in-cisco-catalyst-center)
  - [AI Network Analytics](#121-ai-network-analytics)
  - [Machine Reasoning Engine](#122-machine-reasoning-engine-mre)
  - [AI Endpoint Analytics](#123-ai-endpoint-analytics)
  - [AI-Enhanced Radio Resource Management](#124-ai-enhanced-radio-resource-management-rrm)
- [AI/ML in Network Engineering](#aiml-in-network-engineering)
- [Important Differences to Remember](#important-differences-to-remember)
- [CCNA Exam Quick Review](#ccna-exam-quick-review)
- [Summary](#summary)

---

# What is AI?

## Artificial Intelligence

**Artificial Intelligence (AI)** is the use of computers and computer systems to simulate forms of intelligence that are normally associated with humans.

AI systems can perform tasks such as:

- Pattern recognition
- Learning
- Decision-making
- Problem-solving
- Prediction
- Language processing
- Image recognition
- Recommendation
- Autonomous behaviour

A simple way to think about AI is:

```text
                 Artificial Intelligence
                          |
        +-----------------+------------------+
        |                 |                  |
   Recognition       Decision Making     Problem Solving
        |                 |                  |
   Patterns          Predictions          Actions
```

AI is a broad field. **Machine Learning is one of the major approaches used to achieve AI.**

---

## Examples of AI

Examples of AI applications include:

### Virtual Assistants

- Siri
- Alexa
- Google Assistant

### Recommendation Systems

- Netflix recommendations
- YouTube recommendations
- Amazon product recommendations

### Self-Driving Cars and Robotics

AI can be used to interpret sensor data, recognise objects, make decisions, and control autonomous systems.

Examples include:

- Self-driving vehicles
- Robotics
- Autonomous systems

### Chatbots

Examples include:

- ChatGPT
- Virtual customer-service assistants
- AI-powered support systems

### Game AI

AI can be used to analyse games and develop strategies.

Examples include:

- Stockfish for chess
- AlphaGo for Go

---

## Why AI is Growing

AI has become increasingly important because of:

- Increased computing power
- Availability of large datasets
- Improvements in algorithms
- Advances in machine learning
- Advances in neural networks
- Research breakthroughs
- Increased availability of AI services and tools

---

# What is ML?

## Machine Learning

**Machine Learning (ML) is a subset of Artificial Intelligence.**

Machine Learning focuses on enabling computers to **learn from data and improve their performance without requiring every rule to be explicitly programmed by a human.**

Traditional programming can be represented as:

```text
Rules + Data
     |
     v
 Program
     |
     v
  Output
```

Machine Learning can be represented as:

```text
Training Data
     |
     v
 ML Algorithm
     |
     v
 Learned Model
     |
     v
 Predictions / Decisions
```

The model identifies patterns within the training data and uses those learned patterns to make predictions or decisions about new data.

---

## Examples of Machine Learning

Common examples include:

- Email spam filtering
- Personalised product recommendations
- Fraud detection
- Natural Language Processing (NLP)
- Network anomaly detection
- Network traffic prediction
- Image classification

---

# AI vs ML

The relationship can be visualised as:

```text
+------------------------------------------------+
|            Artificial Intelligence             |
|                                                |
|    +--------------------------------------+    |
|    |          Machine Learning            |    |
|    |                                      |    |
|    |    +----------------------------+    |    |
|    |    |       Deep Learning        |    |    |
|    |    |                            |    |    |
|    |    |   Neural Networks          |    |    |
|    |    +----------------------------+    |    |
|    +--------------------------------------+    |
|                                                |
+------------------------------------------------+
```

### Key relationship

```text
Artificial Intelligence
        |
        +---- Machine Learning
                  |
                  +---- Deep Learning
```

### Important

> **AI is the broader concept. ML is a subset of AI. Deep Learning is a specialised subset of ML.**

---

# Types of Machine Learning

The major machine learning approaches covered in these notes are:

1. Supervised Learning
2. Unsupervised Learning
3. Reinforcement Learning
4. Deep Learning

```text
                     Machine Learning
                            |
        +-------------------+-------------------+
        |                   |                   |
   Supervised         Unsupervised       Reinforcement
    Learning            Learning           Learning
                            |
                       Pattern Finding

                            +
                            
                       Deep Learning
                       Neural Networks
```

---

# Supervised Learning

## Definition

**Supervised Learning** trains a machine learning model using **labelled data**.

Each training example contains:

```text
Input Data + Correct Label
```

The model learns the relationship between the input and the known output.

---

## Example

Suppose we want a model to identify whether an image contains a cat or a dog.

The training data might look like:

```text
Image 1  --->  Cat
Image 2  --->  Dog
Image 3  --->  Cat
Image 4  --->  Dog
Image 5  --->  Cat
```

The labels are already known.

The model studies these examples and learns patterns that allow it to classify new data.

```text
              Labelled Training Data
                       |
             +---------+---------+
             |                   |
          Cat Images          Dog Images
             |                   |
             +---------+---------+
                       |
                       v
                ML Model Training
                       |
                       v
                 Learned Patterns
                       |
                       v
                 New Unseen Data
                       |
                       v
                  Prediction
                       |
                 +-----+-----+
                 |           |
                Cat         Dog
```

---

## Characteristics

Supervised learning uses:

- Labelled datasets
- Known outputs
- Training examples
- Predictions or classifications

---

## Applications

Examples include:

- Spam email detection
- Image classification
- Fraud detection
- Disease prediction
- Network threat detection
- Network fault prediction

---

## Advantages

- Can achieve high accuracy when good labelled data is available.
- Straightforward to understand.
- Suitable for prediction and classification tasks.
- Performance can be measured against known answers.

---

## Disadvantages

- Requires labelled training data.
- Creating labelled datasets can be expensive and time-consuming.
- The model is limited by the quality of the training data.
- The model may not perform well on data that differs significantly from its training data.

---

# Unsupervised Learning

## Definition

**Unsupervised Learning** trains a model using **unlabelled data**.

Unlike supervised learning, there are no predefined correct answers.

The model attempts to discover:

- Patterns
- Relationships
- Structures
- Groups
- Clusters

within the data.

---

## Example

Imagine network traffic containing thousands of connections.

Instead of telling the model:

```text
Traffic A = Normal
Traffic B = Attack
Traffic C = Normal
```

we provide only the traffic data:

```text
Network Traffic
      |
      v
+-----------------------+
| Connection information|
| Packet characteristics|
| Traffic volume        |
| Protocol information  |
+-----------------------+
      |
      v
Unsupervised Learning
      |
      v
Pattern Discovery
      |
      v
+----------+  +----------+
| Cluster 1|  | Cluster 2|
+----------+  +----------+
```

The model may identify groups of traffic with similar characteristics.

---

## Clustering

A common unsupervised learning technique is **clustering**.

The objective is to group similar data points together.

For example:

```text
                Network Traffic

        . . . . .              x x x x
      . . . . . .            x x x x x
       . . . . .              x x x x

             Cluster 1             Cluster 2
```

The algorithm identifies these groups without being explicitly told what each group represents.

---

## Characteristics

Unsupervised learning:

- Uses unlabelled data
- Does not require predefined answers
- Finds hidden patterns
- Can identify groups or clusters
- Can reveal relationships within datasets

---

## Advantages

- Does not require labelled datasets.
- Can reveal hidden patterns.
- Useful for exploratory data analysis.
- Can identify previously unknown groupings.

---

## Disadvantages

- Results can be difficult to interpret.
- The discovered clusters may require human interpretation.
- It can be less straightforward to evaluate than supervised learning.
- The model may identify patterns that are not useful in practice.

---

# Reinforcement Learning

## Definition

**Reinforcement Learning (RL)** trains a model through interaction with an environment.

The model, called an **agent**, takes actions and receives feedback in the form of:

- Rewards
- Penalties

The objective is to learn actions that maximise the long-term reward.

---

## Basic Reinforcement Learning Model

```text
                  +----------------+
                  |   Environment  |
                  +----------------+
                         ^
                         |
                    Reward / Penalty
                         |
                         |
                  +----------------+
                  |      Agent     |
                  +----------------+
                         |
                         |
                       Action
                         |
                         v
                  +----------------+
                  |   Environment  |
                  +----------------+
```

The learning cycle is:

```text
Agent
  |
  | Action
  v
Environment
  |
  | Reward / Penalty
  v
Agent
  |
  | Learns
  v
Better Action
```

---

## How Reinforcement Learning Works

1. The agent observes the environment.
2. The agent selects an action.
3. The environment responds.
4. The agent receives a reward or penalty.
5. The agent learns from the result.
6. The process repeats.
7. Over time, the agent learns which actions produce better outcomes.

---

## Applications

Reinforcement learning can be used in:

### Self-Driving Cars

Learning how to navigate and make decisions based on feedback.

### Game AI

Learning strategies in:

- Chess
- Go
- Video games

### Robotics

Teaching robots to:

- Walk
- Pick up objects
- Navigate
- Perform tasks

---

## Advantages

- Can learn complex behaviours.
- Can adapt to changing environments.
- Does not always require labelled datasets.
- Can optimise decisions over time.

---

## Disadvantages

- Can be resource intensive.
- Training may require many interactions.
- Poorly designed reward systems can produce undesirable behaviour.
- Learning can be inefficient if the environment is complex.

---

# Deep Learning

## Definition

**Deep Learning is a specialised subset of Machine Learning that uses multi-layered artificial neural networks to learn from large and complex datasets.**

Artificial neural networks are computational models inspired by the way biological neural networks process information.

---

## Neural Network Structure

A basic neural network contains:

- Input layer
- Hidden layers
- Output layer

```text
Input Layer          Hidden Layers          Output Layer

   Input 1              ○
                        |
   Input 2 -----------> ○ -----------> ○
                        |
   Input 3              ○
                        |
   Input 4 -----------> ○ -----------> Prediction
```

A deeper network contains multiple hidden layers:

```text
Input
  |
  v
+---------+
| Input   |
| Layer   |
+---------+
     |
     v
+---------+
| Hidden  |
| Layer 1 |
+---------+
     |
     v
+---------+
| Hidden  |
| Layer 2 |
+---------+
     |
     v
+---------+
| Hidden  |
| Layer 3 |
+---------+
     |
     v
+---------+
| Output  |
| Layer   |
+---------+
```

---

## How Deep Learning Works

Data passes through multiple layers of neurons.

Each layer can learn increasingly complex features.

For example, in image recognition:

```text
Raw Image
    |
    v
Basic Features
(edges / shapes)
    |
    v
Intermediate Features
(patterns / structures)
    |
    v
Higher-Level Features
(objects)
    |
    v
Classification
    |
    v
      CAT
```

---

## Deep Learning Can Use Different Learning Approaches

Deep learning models can be trained using:

- Supervised learning
- Unsupervised learning
- Reinforcement learning

---

## Applications

Deep learning is widely used in:

- Image recognition
- Natural Language Processing (NLP)
- Speech recognition
- Autonomous driving
- Computer vision
- Large-scale pattern recognition

---

## Advantages

- Excellent for large and complex datasets.
- Works particularly well with unstructured data such as:
  - Images
  - Audio
  - Text
- Can achieve state-of-the-art performance for many tasks.
- Can automatically learn useful features from data.

---

## Disadvantages

- Resource intensive.
- Can require large datasets.
- Training can require significant computing power.
- Models can behave like a "black box", making their decisions difficult to interpret.

---

# Predictive and Generative AI

AI applications can be broadly understood through two important capabilities:

```text
Artificial Intelligence
          |
          v
   Machine Learning
          |
     +----+----+
     |         |
     v         v
Predictive   Generative
   AI           AI
```

---

# Predictive AI

## Definition

**Predictive AI uses machine learning to analyse historical data and predict future outcomes, events, or trends.**

The basic process is:

```text
Historical Data
      |
      v
Machine Learning
      |
      v
Identify Patterns
      |
      v
Prediction
      |
      v
Future Outcome
```

---

## Examples

### Healthcare

Predicting:

- Patient outcomes
- Disease progression

### Network Security

Detecting:

- Anomalies
- Suspicious activity
- Potential security threats

### Traffic Management

Predicting:

- Traffic congestion
- Traffic patterns

### Business Forecasting

Predicting:

- Sales trends
- Customer behaviour

### Weather Forecasting

Using historical and current meteorological information to predict future weather conditions.

---

## Predictive AI in Networking

Predictive AI can analyse historical network information to identify patterns that may indicate future problems.

For example:

```text
Historical Network Data
          |
          v
Traffic + CPU + Memory
+ Errors + Latency
          |
          v
Predictive Model
          |
          v
Pattern Identified
          |
          v
Potential Future Problem
```

---

## Advantages

- Improves decision-making.
- Provides actionable insights.
- Can identify potential problems before they occur.
- Can help with proactive network management.

---

## Disadvantages

- Requires high-quality historical data.
- Prediction accuracy depends on the quality of the data.
- Historical patterns may not always represent future conditions.
- Unexpected events can reduce prediction accuracy.

---

# Generative AI

## Definition

**Generative AI uses machine learning to learn patterns from existing data and generate new content.**

Unlike predictive AI, which primarily focuses on predicting an outcome, generative AI can create new content.

---

## Types of Generated Content

Generative AI can produce:

- Text
- Images
- Audio
- Video
- Code
- Scripts
- Documentation

---

## Examples

### Text Generation

- ChatGPT
- Gemini
- Copilot

### Image Generation

- Midjourney
- DALL-E

### Video Generation

- Sora
- Veo

---

## Basic Generative AI Process

```text
Training Data
     |
     v
Learn Patterns
     |
     v
Generative Model
     |
     v
Prompt
     |
     v
Generated Content
```

For example:

```text
Prompt:
"Generate an image of a cat."

             |
             v

        Generative AI
             |
             v

       New Image Output
```

---

## Advantages

- Useful for creative tasks.
- Can automate content creation.
- Can generate text, images, code, documentation, and other content.
- Can assist humans with tasks that would otherwise require significant time.

---

## Disadvantages

- Generated content can contain errors.
- Can be misused.
- Can produce deepfakes.
- Can raise plagiarism and copyright concerns.
- Output quality depends on the quality and characteristics of the training data.

---

# AI Hallucinations

A major limitation of Generative AI is **hallucination**.

An AI hallucination occurs when an AI system generates information that appears plausible or confident but is actually incorrect, unsupported, or fabricated.

For example:

```text
User
 |
 | Question
 v
Generative AI
 |
 v
Generated Answer
 |
 +---- Correct information
 |
 +---- Incorrect information
 |
 +---- Fabricated information
        ^
        |
     Hallucination
```

### Important for Network Engineers

A network engineer should **not blindly trust AI-generated configuration or troubleshooting advice**.

For example, AI might generate:

```text
interface GigabitEthernet0/1
some-command-that-does-not-exist
```

Therefore:

> **Always verify AI-generated technical information against official documentation, device output, configuration requirements, and lab testing before using it in a production network.**

---

# Predictive and Generative AI in Networks

AI can support network engineering in two different ways.

```text
                    AI in Networking
                           |
             +-------------+-------------+
             |                           |
             v                           v
       Predictive AI              Generative AI
             |                           |
       Analyse data                 Create content
             |                           |
      Predict outcomes          Assist engineers
```

---

# Predictive AI in Networking

## 1. Traffic Forecasting

Predict network traffic patterns to:

- Optimise bandwidth allocation
- Identify potential congestion
- Improve capacity planning
- Plan network upgrades

Example:

```text
Historical Traffic
       |
       v
Traffic Analysis
       |
       v
Predict Future Traffic
       |
       v
Potential Congestion
       |
       v
Proactive Action
```

---

## 2. Security Threat Detection

Predictive AI can identify abnormal or suspicious traffic patterns.

For example:

```text
Normal Traffic
      |
      v
Network Monitoring
      |
      v
ML Model
      |
      +---- Normal Pattern
      |
      +---- Anomalous Pattern
                  |
                  v
             Investigation
```

Potential applications include:

- Anomaly detection
- Suspicious traffic identification
- Threat detection
- Security monitoring

---

## 3. Predictive Maintenance

AI can analyse historical and current device performance to identify potential hardware or network failures.

For example:

```text
Device Metrics
      |
      +---- CPU
      +---- Memory
      +---- Temperature
      +---- Interface Errors
      +---- Traffic
      |
      v
Predictive Model
      |
      v
Potential Failure
      |
      v
Proactive Maintenance
```

The goal is to reduce downtime by identifying problems before they become major failures.

---

# Generative AI in Networking

## 1. Network Documentation

Generative AI can assist in creating documentation such as:

- Network configuration documentation
- Network policies
- Device descriptions
- Troubleshooting notes
- Network diagrams descriptions

---

## 2. Configuration Generation

Generative AI can help create network configurations based on a desired requirement.

For example:

```text
Requirement
     |
     v
"Create VLAN 20 for Sales"
     |
     v
Generative AI
     |
     v
Cisco Configuration
```

Example output:

```cisco
vlan 20
 name SALES
```

However:

> AI-generated configurations must always be reviewed and tested before being deployed.

---

## 3. Network Design

Generative AI can assist network engineers by suggesting:

- Network layouts
- VLAN structures
- Addressing approaches
- Network modifications
- Design alternatives

The engineer remains responsible for validating the design.

---

## 4. Troubleshooting

Generative AI can assist with troubleshooting by analysing:

- Error messages
- Logs
- Device output
- Configuration snippets
- Symptoms

Example:

```text
Router / Switch Output
          |
          v
       AI Model
          |
          v
Possible Cause
          |
          v
Suggested Solution
          |
          v
Engineer Verification
```

---

## 5. Script Generation

Generative AI can assist with creating:

- Python scripts
- Network automation scripts
- Configuration templates
- Bash scripts
- API-related code

For example:

```text
Network Requirement
        |
        v
Generative AI
        |
        v
Python / Automation Script
        |
        v
Engineer Review
        |
        v
Testing
        |
        v
Deployment
```

---

# Predictive AI vs Generative AI in Networking

| Feature | Predictive AI | Generative AI |
|---|---|---|
| Main purpose | Predict outcomes | Create new content |
| Input | Historical/current data | Data + prompt/instructions |
| Output | Prediction/forecast | Text, code, configuration, documentation, etc. |
| Network traffic | Predict congestion | Explain traffic patterns |
| Security | Detect anomalies | Explain security events |
| Maintenance | Predict failures | Generate maintenance documentation |
| Configuration | Analyse configuration behaviour | Generate configuration examples |
| Troubleshooting | Predict possible failures | Suggest troubleshooting steps |
| Documentation | Analyse existing data | Generate documentation |

---

# AI in Cisco Catalyst Center

## Overview

**Cisco Catalyst Center** (formerly known as **Cisco DNA Center**) includes AI-enabled capabilities designed to help network administrators identify issues, understand network behaviour, improve performance, and improve operational efficiency.

The major AI-related capabilities covered in these notes are:

1. AI Network Analytics
2. Machine Reasoning Engine (MRE)
3. AI Endpoint Analytics
4. AI-Enhanced Radio Resource Management (RRM)

```text
                 Cisco Catalyst Center
                         |
       +-----------------+------------------+
       |                 |                  |
       v                 v                  v
AI Network          Machine Reasoning   AI Endpoint
Analytics              Engine (MRE)      Analytics
       |
       |
       +-------------------------------+
                                       |
                                       v
                         AI-Enhanced Radio
                         Resource Management
                                (RRM)
```

---

# 12.1 AI Network Analytics

## Definition

**AI Network Analytics** uses AI to establish a baseline of normal network behaviour.

The system can then continuously monitor network activity and identify deviations from the expected behaviour.

---

## Basic Concept

```text
Network Data
     |
     v
AI Network Analytics
     |
     v
Establish Normal Baseline
     |
     v
Continuous Monitoring
     |
     v
Compare Current Behaviour
     |
     +----------+-----------+
     |                      |
 Normal                  Anomaly
     |                      |
     v                      v
Continue              Investigation /
Monitoring             Recommendation
```

---

## Functions

AI Network Analytics can:

- Establish baseline network behaviour.
- Monitor network activity.
- Identify abnormal behaviour.
- Detect and predict anomalies.
- Provide insights.
- Provide recommendations for improving network performance.

---

## Example

Suppose a network normally experiences:

```text
Normal CPU utilisation:
20% - 40%

Normal latency:
5 ms - 10 ms

Normal interface errors:
Very low
```

If the system detects behaviour significantly different from the normal baseline, it can identify this as an anomaly.

```text
Normal Baseline
      |
      v
Current Network Behaviour
      |
      v
Compare
      |
      +---- Matches baseline ---> Normal
      |
      +---- Significant difference ---> Anomaly
```

---

# 12.2 Machine Reasoning Engine (MRE)

## Definition

The **Machine Reasoning Engine (MRE)** uses AI to perform **root-cause analysis** when network problems occur.

Instead of simply reporting that something is wrong, the system attempts to determine the likely cause of the problem and can suggest possible resolutions.

---

## Basic Concept

```text
Network Problem
      |
      v
Machine Reasoning Engine
      |
      v
Analyse Network Information
      |
      v
Root-Cause Analysis
      |
      v
Possible Cause
      |
      v
Suggested Resolution
```

---

## Example

Imagine an interface goes down.

```text
Interface Down
      |
      v
MRE
      |
      +---- Analyse device
      +---- Analyse interfaces
      +---- Analyse network relationships
      +---- Analyse available information
      |
      v
Root Cause
      |
      v
Suggested Resolution
```

---

## Benefits

MRE can:

- Perform root-cause analysis.
- Identify possible causes of network problems.
- Suggest resolutions.
- Potentially assist with automated corrective actions.
- Reduce troubleshooting time.
- Reduce network downtime.

---

## Important Concept

### AI Network Analytics vs MRE

These two features have different purposes.

```text
AI Network Analytics
        |
        v
"What is abnormal?"
```

```text
Machine Reasoning Engine
        |
        v
"Why did the problem happen?"
```

A simple way to remember it:

> **Analytics identifies abnormal behaviour. MRE helps determine the root cause.**

---

# 12.3 AI Endpoint Analytics

## Definition

**AI Endpoint Analytics** identifies and classifies devices connected to the network.

It provides network administrators with greater visibility into connected endpoints.

---

## Basic Concept

```text
                     Network
                        |
        +---------------+---------------+
        |               |               |
        v               v               v
      Laptop          Phone            IoT
        |               |               |
        +---------------+---------------+
                        |
                        v
              AI Endpoint Analytics
                        |
                        v
                Device Classification
```

---

## Functions

AI Endpoint Analytics can:

- Identify devices.
- Classify devices.
- Provide endpoint visibility.
- Detect unauthorised devices.
- Detect unusual endpoint behaviour.
- Simplify device onboarding.
- Assist with automated profiling.
- Assist with segmentation.

---

## Example

A device joins the network:

```text
New Device
     |
     v
AI Endpoint Analytics
     |
     v
Device Identification
     |
     v
Device Classification
     |
     +---- Laptop
     +---- Smartphone
     +---- Printer
     +---- IoT Device
     +---- Other
```

This provides administrators with greater visibility into what is connected to the network.

---

# 12.4 AI-Enhanced Radio Resource Management (RRM)

## Definition

**Radio Resource Management (RRM)** is used to optimise wireless network performance.

AI-enhanced RRM can dynamically adjust wireless radio settings to improve wireless performance.

---

## Main Objectives

AI-enhanced RRM can help:

- Optimise wireless performance.
- Balance wireless load.
- Reduce interference.
- Improve wireless coverage.
- Dynamically adjust radio settings.

---

## Basic Concept

```text
Wireless Network
       |
       v
Monitor Wireless Environment
       |
       +---- Channel utilisation
       +---- Interference
       +---- Client load
       +---- Coverage
       |
       v
AI-Enhanced RRM
       |
       v
Optimise Radio Settings
       |
       +---- Reduce interference
       +---- Balance load
       +---- Improve coverage
       |
       v
Improved Wireless Performance
```

---

## Wireless Optimisation

For example, if an access point is experiencing excessive interference, AI-enhanced RRM can help optimise radio settings to improve the wireless environment.

```text
High Interference
       |
       v
AI-Enhanced RRM
       |
       v
Analyse Wireless Environment
       |
       v
Optimise Radio Settings
       |
       v
Reduced Interference
```

---

# AI/ML in Network Engineering

AI and ML can support network engineers across several areas.

| Network Area | AI/ML Application |
|---|---|
| Network Monitoring | Detect abnormal behaviour |
| Traffic Management | Predict traffic patterns |
| Security | Detect suspicious activity |
| Maintenance | Predict possible failures |
| Troubleshooting | Analyse problems and suggest causes |
| Endpoint Management | Identify and classify devices |
| Wireless | Optimise radio resources |
| Documentation | Generate documentation |
| Configuration | Generate configuration examples |
| Automation | Generate scripts |
| Network Design | Suggest design alternatives |
| Capacity Planning | Predict future requirements |

---

# AI/ML Network Engineer Workflow

A modern network engineer can use AI as an assistant while still maintaining responsibility for network decisions.

```text
              Network Data
                   |
                   v
             AI / ML System
                   |
       +-----------+-----------+
       |                       |
       v                       v
   Prediction               Generation
       |                       |
       v                       v
Possible Issue            Suggested Output
       |                       |
       +-----------+-----------+
                   |
                   v
            Network Engineer
                   |
                   v
              Verification
                   |
                   v
                Testing
                   |
                   v
              Deployment
```

The important part is the final verification by the engineer.

---

# Important Differences to Remember

## AI vs ML

```text
AI
|
+-- Broad field of simulating intelligent behaviour
|
+-- ML
    |
    +-- Learns from data
```

**Remember:**

> Machine Learning is a subset of Artificial Intelligence.

---

## Machine Learning vs Deep Learning

| Machine Learning | Deep Learning |
|---|---|
| Broad ML field | Specialised subset of ML |
| Can use many algorithms | Uses multi-layer neural networks |
| Can work with smaller datasets depending on task | Often benefits from large datasets |
| Often easier to interpret | Can be difficult to interpret |
| Generally less computationally demanding | Often computationally intensive |

---

## Supervised vs Unsupervised

| Supervised | Unsupervised |
|---|---|
| Uses labelled data | Uses unlabelled data |
| Correct answers are provided | No predefined answers |
| Learns from known examples | Finds patterns |
| Classification/prediction | Clustering/pattern discovery |

### Easy memory trick

```text
SUPERVISED
    |
    v
Teacher provides answers
    |
    v
Labelled Data


UNSUPERVISED
    |
    v
No teacher / no labels
    |
    v
Find the patterns
```

---

## Reinforcement Learning

Remember:

```text
Agent
  |
  v
Action
  |
  v
Environment
  |
  v
Reward / Penalty
  |
  v
Learning
```

### Key word:

> **Reward / Penalty**

---

## Deep Learning

Remember:

> **Deep Learning = Multi-layer Neural Networks**

```text
Input
  |
  v
Hidden Layer
  |
  v
Hidden Layer
  |
  v
Hidden Layer
  |
  v
Output
```

---

## Predictive AI

Remember:

> **Predictive AI = Predict what may happen**

Examples:

- Network traffic forecasting
- Threat detection
- Predictive maintenance
- Weather forecasting

---

## Generative AI

Remember:

> **Generative AI = Generate something new**

Examples:

- Text
- Images
- Video
- Code
- Network documentation
- Network configurations
- Scripts

---

# Cisco Catalyst Center Quick Memory Guide

The four important AI capabilities from these notes can be remembered as:

```text
AI Network Analytics
        |
        v
Find abnormal behaviour


Machine Reasoning Engine
        |
        v
Find the root cause


AI Endpoint Analytics
        |
        v
Identify and classify endpoints


AI-Enhanced RRM
        |
        v
Optimise wireless radio resources
```

---

# CCNA Exam Quick Review

## Question 1

**Which type of ML uses labelled data?**

Answer:

> **Supervised Learning**

---

## Question 2

**Which type of ML uses unlabelled data to discover patterns?**

Answer:

> **Unsupervised Learning**

---

## Question 3

**Which type of ML uses rewards and penalties?**

Answer:

> **Reinforcement Learning**

---

## Question 4

**Which type of ML uses multi-layered neural networks?**

Answer:

> **Deep Learning**

---

## Question 5

**Which AI approach predicts future outcomes based on historical data?**

Answer:

> **Predictive AI**

---

## Question 6

**Which AI approach generates new content?**

Answer:

> **Generative AI**

---

## Question 7

**What is a major risk associated with Generative AI?**

Answer:

> **AI hallucinations**, where the system can generate information that appears plausible but is incorrect or fabricated.

---

## Question 8

**Which Cisco Catalyst Center feature uses AI for root-cause analysis?**

Answer:

> **Machine Reasoning Engine (MRE)**

---

## Question 9

**Which Cisco Catalyst Center feature identifies and classifies network endpoints?**

Answer:

> **AI Endpoint Analytics**

---

## Question 10

**Which Cisco Catalyst Center capability helps optimise wireless radio resources?**

Answer:

> **AI-Enhanced Radio Resource Management (RRM)**

---

## Question 11

**Which Cisco Catalyst Center capability establishes a baseline of normal network behaviour and identifies anomalies?**

Answer:

> **AI Network Analytics**

---

# Quick Comparison Table

| Concept | Key Idea | Easy Memory |
|---|---|---|
| AI | Simulates intelligent behaviour | Intelligence |
| ML | Learns from data | Learning |
| Supervised | Learns from labelled data | Teacher |
| Unsupervised | Finds patterns in unlabelled data | Discover |
| Reinforcement | Learns from rewards/penalties | Reward |
| Deep Learning | Multi-layer neural networks | Neural networks |
| Predictive AI | Predicts future outcomes | Predict |
| Generative AI | Creates new content | Generate |
| AI Hallucination | Incorrect/fabricated AI output | Verify |
| AI Network Analytics | Finds abnormal network behaviour | Detect |
| MRE | Root-cause analysis | Why? |
| AI Endpoint Analytics | Identifies/classifies endpoints | Who/What? |
| AI-Enhanced RRM | Optimises wireless radio resources | Wireless |

---

# AI/ML Concept Map

```text
                         Artificial Intelligence
                                  |
                    +-------------+-------------+
                    |                           |
                    v                           v
             Machine Learning            Other AI Methods
                    |
          +---------+---------+----------------+
          |         |         |                |
          v         v         v                v
     Supervised  Unsupervised Reinforcement  Deep Learning
          |         |         |                |
          |         |         |                |
       Labels     Patterns   Rewards       Neural Networks
          |         |         |
          +---------+---------+
                    |
                    v
            Modern AI Applications
                    |
              +-----+------+
              |            |
              v            v
         Predictive     Generative
             AI             AI
              |              |
              v              v
        Predict Future    Create Content
              |              |
              +------+-------+
                     |
                     v
              Network Engineering
                     |
      +--------------+--------------+
      |              |              |
      v              v              v
   Analytics     Security       Automation
      |              |              |
      v              v              v
 Catalyst Center / Network Operations
                     |
      +--------------+----------------+
      |              |                |
      v              v                v
AI Network       MRE            AI Endpoint
Analytics                        Analytics
                     |
                     v
               AI-Enhanced RRM
```

---

# AI/ML and the Network Engineer

AI and ML do not replace the fundamental networking knowledge required by a network engineer.

A network engineer still needs to understand:

- Ethernet
- VLANs
- Trunking
- STP/RSTP
- IPv4
- IPv6
- Subnetting
- VLSM
- Routing
- OSPF
- EIGRP
- DHCP
- NAT
- ACLs
- Wireless networking
- Network security
- Troubleshooting

AI and ML can instead become additional tools that help the engineer analyse information and automate tasks.

```text
Networking Knowledge
        +
AI / ML Knowledge
        +
Automation
        |
        v
Modern Network Engineer
```

---

# Practical Example: AI-Assisted Network Troubleshooting

Imagine users report slow network performance.

A traditional troubleshooting process might be:

```text
User Complaint
      |
      v
Check Interface
      |
      v
Check Errors
      |
      v
Check CPU / Memory
      |
      v
Check Latency
      |
      v
Check Traffic
      |
      v
Identify Cause
      |
      v
Fix Problem
```

AI-assisted troubleshooting could add another layer:

```text
Network Data
     |
     +---- Interface Statistics
     +---- CPU / Memory
     +---- Traffic
     +---- Errors
     +---- Latency
     +---- Logs
     |
     v
AI / ML Analysis
     |
     v
Anomaly Detection
     |
     v
Possible Root Cause
     |
     v
Suggested Troubleshooting
     |
     v
Network Engineer
     |
     v
Verification
```

The engineer still needs to validate the result.

---

# Practical Example: Predictive Network Maintenance

A network administrator wants to identify devices that may fail in the future.

The system can analyse:

```text
Historical Data
       |
       +---- CPU
       +---- Memory
       +---- Temperature
       +---- Interface Errors
       +---- Traffic
       +---- Device Events
       |
       v
Machine Learning Model
       |
       v
Identify Patterns
       |
       v
Predict Potential Failure
       |
       v
Maintenance Before Failure
```

This changes network operations from:

> **Reactive troubleshooting**

to:

> **Proactive network management**

---

# Practical Example: Generative AI for Network Configuration

Suppose a network engineer needs a VLAN configuration.

The engineer provides a requirement:

```text
Create VLAN 20
Name: SALES
```

Generative AI could produce:

```cisco
configure terminal

vlan 20
 name SALES

end
```

The engineer should then:

1. Review the generated configuration.
2. Verify the commands.
3. Test the configuration.
4. Confirm the design requirements.
5. Deploy only after validation.

---

# Important Security Consideration

AI should be treated as an **assistant**, not as an unquestionable authority.

Never blindly deploy AI-generated network configurations.

A safe workflow is:

```text
AI Suggestion
     |
     v
Engineer Review
     |
     v
Official Documentation
     |
     v
Lab Testing
     |
     v
Validation
     |
     v
Production Deployment
```

This is particularly important because generative AI can produce:

- Incorrect commands
- Incorrect assumptions
- Outdated information
- Non-existent commands
- Unsafe configurations
- Hallucinated technical information

---

# Summary

## Artificial Intelligence

AI uses computers to simulate intelligent behaviour such as:

- Pattern recognition
- Learning
- Decision-making
- Problem-solving

---

## Machine Learning

ML is a subset of AI that allows computers to learn patterns from data and improve without requiring every rule to be explicitly programmed.

---

## Supervised Learning

Uses **labelled data** to make predictions or classifications.

```text
Labelled Data
     |
     v
Training
     |
     v
Prediction
```

---

## Unsupervised Learning

Uses **unlabelled data** to discover patterns, relationships, or groups.

```text
Unlabelled Data
     |
     v
Pattern Discovery
     |
     v
Clusters / Relationships
```

---

## Reinforcement Learning

Learns through **actions, rewards, and penalties**.

```text
Action
  |
  v
Environment
  |
  v
Reward / Penalty
  |
  v
Learning
```

---

## Deep Learning

A specialised subset of ML that uses **multi-layered neural networks** to process large and complex datasets.

---

## Predictive AI

Uses historical data to predict future outcomes.

Network examples include:

- Traffic forecasting
- Threat detection
- Predictive maintenance

---

## Generative AI

Learns patterns from existing data and creates new content.

Network examples include:

- Documentation generation
- Configuration generation
- Troubleshooting assistance
- Network design assistance
- Script generation

---

## Cisco Catalyst Center

Cisco Catalyst Center includes several AI-enabled capabilities:

```text
AI Network Analytics
        |
        v
Baseline + Anomaly Detection


Machine Reasoning Engine
        |
        v
Root-Cause Analysis


AI Endpoint Analytics
        |
        v
Endpoint Identification + Classification


AI-Enhanced RRM
        |
        v
Wireless Optimisation
```

---

# Final Takeaway

The most important concepts to remember are:

```text
AI
 |
 +-- ML
      |
      +-- Supervised
      |     |
      |     +-- Labelled Data
      |
      +-- Unsupervised
      |     |
      |     +-- Unlabelled Data
      |     +-- Pattern Discovery
      |
      +-- Reinforcement
      |     |
      |     +-- Reward / Penalty
      |
      +-- Deep Learning
            |
            +-- Neural Networks
```

And:

```text
Predictive AI
     |
     +-- Predict future outcomes
     +-- Traffic forecasting
     +-- Threat detection
     +-- Predictive maintenance


Generative AI
     |
     +-- Create new content
     +-- Documentation
     +-- Configuration
     +-- Troubleshooting
     +-- Scripts
```

For Cisco Catalyst Center:

```text
AI Network Analytics
        = Detect abnormal behaviour

MRE
        = Root-cause analysis

AI Endpoint Analytics
        = Identify and classify endpoints

AI-Enhanced RRM
        = Optimise wireless radio resources
```

> **Key CCNA memory point:**  
> **Supervised = labelled data**  
> **Unsupervised = unlabelled data and patterns**  
> **Reinforcement = rewards and penalties**  
> **Deep Learning = multi-layer neural networks**  
> **Predictive AI = predicts**  
> **Generative AI = generates**  
> **MRE = root-cause analysis**  
> **AI Endpoint Analytics = endpoint identification/classification**  
> **AI Network Analytics = baseline and anomaly detection**  
> **AI-Enhanced RRM = wireless optimisation**

---

# Personal Learning Note

This topic connects AI/ML with my broader Network Engineering studies. Understanding these concepts helps me see how traditional networking is increasingly combined with:

- Artificial Intelligence
- Machine Learning
- Network Automation
- Network Analytics
- Cybersecurity
- Predictive Maintenance
- Wireless Optimisation

The goal is not to replace fundamental networking knowledge with AI, but to understand how AI and ML can be used as additional tools to make network operations more **proactive, intelligent, automated, and efficient**.
