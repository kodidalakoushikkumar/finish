# COMPLETE ARTIFICIAL INTELLIGENCE TREE

```
ARTIFICIAL INTELLIGENCE
│
├── 1) Symbolic / Classical AI
│     ├── Rule-Based Systems
│     ├── Expert Systems
│     ├── Knowledge Representation
│     ├── Logic Programming
│     └── Search Algorithms
│
├── 2) Machine Learning
│     ├── Supervised Learning
│     │      ├── Regression
│     │      └── Classification
│     │
│     ├── Unsupervised Learning
│     │      ├── Clustering
│     │      ├── Dimensionality Reduction
│     │      └── Association Rules
│     │
│     ├── Semi-Supervised Learning
│     ├── Self-Supervised Learning
│     ├── Reinforcement Learning
│     │      ├── Q-Learning
│     │      ├── Policy Learning
│     │      └── Deep Reinforcement Learning
│     │
│     └── Deep Learning
│            ├── Neural Networks (ANN)
│            │      ├── Feedforward Networks
│            │      ├── Backpropagation
│            │      └── Optimization Algorithms
│            │
│            ├── CNN (Vision Models)
│            │      ├── Object Detection
│            │      ├── Image Segmentation
│            │      └── Face Recognition
│            │
│            ├── RNN (Sequence Models)
│            │      ├── LSTM
│            │      └── GRU
│            │
│            ├── Generative Models
│            │      ├── Autoencoders
│            │      ├── VAEs
│            │      ├── GANs
│            │      └── Diffusion Models
│            │
│            └── Transformers
│                   ├── Encoder Models (BERT)
│                   ├── Decoder Models (GPT)
│                   ├── Encoder-Decoder (T5)
│                   └── Large Language Models (LLMs)
│
├── 3) Natural Language Processing
│     ├── Text Classification
│     ├── Named Entity Recognition
│     ├── Machine Translation
│     ├── Question Answering
│     ├── Summarization
│     └── Chatbots / Assistants
│
├── 4) Computer Vision
│     ├── Image Classification
│     ├── Object Detection
│     ├── Tracking
│     ├── OCR (text from image)
│     └── Video Analysis
│
├── 5) Speech & Audio AI
│     ├── Speech Recognition
│     ├── Text-to-Speech
│     ├── Speaker Identification
│     └── Sound Classification
│
├── 6) Robotics
│     ├── Motion Planning
│     ├── SLAM (mapping & navigation)
│     ├── Manipulation
│     └── Autonomous Driving
│
├── 7) Planning & Optimization
│     ├── Path Finding
│     ├── Scheduling
│     ├── Resource Allocation
│     └── Game Playing
│
├── 8) Multi-Agent Systems
│     ├── Swarm Intelligence
│     ├── Distributed AI
│     └── Cooperative Agents
│
└── 9) Human-AI Interaction
      ├── Recommendation Systems
      ├── Personal Assistants
      └── Human Feedback Learning

```

# 1) Supervised Learning
You give the machine: **Input + Correct Output (answers)**
It learns the mapping.  `x → y email → spam photo → cat house features → price`
Think: teacher supervising a student.
## A) Regression (predict a number)
Output is continuous value.
Examples:
- House price prediction
- Temperature forecasting
- Sales prediction
- Stock value estimation
### How it learns
Finds mathematical relationship:  `price = 2*(rooms) + 500*(area) + noise`
Algorithms:
- Linear Regression
- Polynomial Regression
- Ridge / Lasso
- Random Forest Regressor
👉 Used heavily in business analytics & forecasting
## B) Classification (predict a category)
Output is a label.
Examples:
- Spam / Not Spam
- Fraud / Legit
- Disease / Healthy
- Churn / Not churn
Algorithms:
- Logistic Regression
- Decision Tree
- Random Forest
- SVM
- k-Nearest Neighbor
- Naive Bayes
👉 Most common real-world ML task
# 2) Unsupervised Learning
You give **only data — no answers**
Machine discovers structure itself.
Think: grouping unknown objects in a box.
## A) Clustering (group similar items)
Example:  
Customers grouped by buying behavior
`Group A → rich customers Group B → discount seekers Group C → rare buyers`
Algorithms:
- K-Means
- Hierarchical Clustering
- DBSCAN
Used in:
- Marketing segmentation
- Fraud anomaly detection
- Social network analysis
## B) Dimensionality Reduction (compress data)
High-feature data → fewer features while keeping information.
Example:   1000 features → 10 meaningful features
Algorithms:
- PCA
- t-SNE
- UMAP
Used in:
- Visualization
- Speeding up models
- Noise removal
## C) Association Rules (pattern relationships)
Finds “people who buy X also buy Y”
Example:  `Beer → Diapers Laptop → Mouse Phone → Case`
Algorithm:
- Apriori
- FP-Growth
Used in recommender systems.
# 3) Semi-Supervised Learning
Small labeled data + large unlabeled data.
Because labeling is expensive.
Example:   1000 labeled medical scans + 1 million unlabeled scans.
Used in:
- Medical AI
- Industrial inspection
# 4) Self-Supervised Learning (Modern AI magic)
Model creates its own labels.
Example:   Hide word in sentence → prdict missing word
`"The cat is on the ___"`
This is how modern language models learn before training.
Used by models from OpenAI and Google.
# 5) Reinforcement Learning
Learning by **reward and punishment**
Agent interacts with environment.
`action → reward → learn`
Example:  
Robot walking:
- falls → bad reward
- stable → good reward    
Used in:
- Game AI
- Robotics
- Traffic control
- Trading systems
## Types
### Value-based
Learn value of each action  
(eg: Q-Learning)
### Policy-based
Learn best behavior directly
### Deep Reinforcement Learning
Neural networks + RL  
Used in advanced game AIs.
# 6) Deep Learning (subset of ML)
When dataset becomes huge → traditional ML fails.
So we use neural networks.
## Inside Deep Learning

- Neural Networks → general patterns
- CNN → images
- RNN → sequences/time
- Transformers → language/context
- Generative Models → create data

# SIMPLE MEMORY MAP

|Problem|ML Type|
|---|---|
|Predict number|Regression|
|Predict category|Classification|
|Find hidden groups|Clustering|
|Compress data|Dimensionality Reduction|
|Recommend items|Association Rules|
|Learn from rewards|Reinforcement Learning|
|Learn from massive raw data|Deep Learning|

# One-line intuition

> Supervised = learn from teacher  
> Unsupervised = discover patterns  
> Reinforcement = learn from experience  
> Deep Learning = learn complex patterns automatically

## 1) Artificial Intelligence (AI)
**Goal:** Make machines behave intelligently (like humans)
This does NOT always mean learning.
Examples:
- Rule-based chatbot: “If user says hello → reply hello”
- Chess engine calculating best move
- Face unlock in phone
- Spam detection
👉 AI is the **entire field** — biggest umbrella.
So:
> All ML is AI  
> But not all AI is ML
## 2) Machine Learning (ML)
Machines **learn patterns from data instead of hardcoding rules**
Instead of:  `if email contains "lottery" -> spam`
We do:  `Show 1 million emails → machine learns what spam looks like`
Examples:
- Netflix recommendations
- Credit card fraud detection
- Stock prediction
- Voice recognition
👉 ML = subset of AI that learns from data
## 3) Deep Learning (DL)
A special type of ML using **layers of math neurons**
Normal ML: Uses human-chosen features
Deep Learning:  Finds features automatically
Example:   You teach computer “cat”
Traditional ML: You manually tell: ears shape, tail, eyes
Deep Learning:  Show 10 million images → it figures everything

Used in:
- Speech recognition
- Image recognition
- Chatbots
- Self driving
👉 DL = subset of ML
## 4) Neural Networks
The **algorithm inside Deep Learning**
Inspired by human brain neurons: `Input → Hidden Layers → Output`
Each layer learns patterns:
- Layer 1: edges
- Layer 5: shapes
- Layer 20: faces
- Layer 100: emotions
So:

> Neural Networks are the ENGINE  
> Deep Learning is the CAR

## 5) Transformers (Big Breakthrough — 2017)
A new neural network design from  
Google research paper **“Attention Is All You Need”**
They understand relationships between words instead of sequence memory.
Old models:  read word by word
Transformers:   read entire sentence at once
That’s why modern AI understands context.
## 6) GPT (Generative Pre-trained Transformer)
Created by OpenAI
GPT is a **type of transformer model specialized in language generation**
What it does:   Predict next word repeatedly
Example:   `"I drank coffee because I was..." → tired`
After trillions of predictions → becomes ChatGPT.
So:

> GPT is NOT AI  
> GPT is NOT ML  
> GPT is NOT Deep Learning

It is:   One specific model inside Deep Learning