# Autonomous-Driving-Foundation-Stack-Student-Edition-
This project demonstrates an end-to-end understanding of how a modern self-driving system works — starting from raw camera video and ending with a refined driving policy.
# Autonomous Driving Foundation Stack (Student Edition)

A **camera-only autonomous driving pipeline** showcasing multi-task perception, end-to-end imitation learning, offline reinforcement learning, and a lightweight data engine.  

---

## 🚗 Project Summary
This project demonstrates an end-to-end understanding of how a modern self-driving system works — starting from raw camera video and ending with a refined driving policy.

It includes:
- **Multi-task video perception** (lane segmentation + steering prediction)
- **End-to-end imitation learning** on real driving data
- **Offline reinforcement learning** to make the policy safer and more stable
- **A lightweight data engine** for filtering and improving training data
- **Optional generative augmentation** for rare driving scenarios

The goal is not to build a production system, but to create a **clear, research-style, educational autonomy stack**.

---

## 🧩 Core Modules
### 1) Multi-Task Video Perception (`perception/`)
A compact video backbone (3D CNN or TimeSformer-lite) jointly predicts:
- Lane segmentation
- Steering angle

This module demonstrates **multi-task learning**, **video modeling**, and **shared encoder design**.

### 2) End-to-End Imitation Learning (`imitation_learning/`)
Uses real driving data (e.g., comma.ai) to learn human driving behavior:
- **Input:** short video clip
- **Output:** steering angle (and optionally throttle/brake)

Implements temporal modeling via **LSTM** or **3D CNN**.

### 3) Offline Reinforcement Learning (`offline_rl/`)
Refines the imitation policy with offline RL:
- Behavior Cloning (baseline)
- Conservative Q-Learning (CQL) or Implicit Q-Learning (IQL)

Focus: policy stability, safety, reduced interventions.

### 4) Data Engine + Synthetic Data (`data_engine/`)
A small but powerful data-centric module:
- Confidence-based sample filtering
- Identification of poor/ambiguous frames
- Optional diffusion-based synthetic data generation for rare scenarios

This simulates how real autonomy teams maintain **high-quality datasets**.

---

## 🏗️ Architecture Diagram
```
Raw Driving Video → Data Engine → Perception Model → Imitation Policy → Offline RL Policy → Simulator Demo
```

Detailed view:
```
                +---------------------------+
                |    Raw Driving Dataset    |
                +-------------+-------------+
                              |
                              v
                   +-------------------+
                   |     Data Engine   |
                   +---------+---------+
                             |
                +------------+------------+
                |                         |
                v                         v
      +--------------------+    +----------------------+
      | Perception Model   |    | Imitation Policy     |
      +---------+----------+    +----------+-----------+
                |                          |
                +------------+-------------+
                             v
                   +----------------------+
                   |   Offline RL Policy  |
                   +----------+-----------+
                              |
                              v
                      +---------------+
                      |   Simulator   |
                      +---------------+
```

---

## 🔧 Tech Stack
- **Python**, PyTorch
- 3D CNN or lightweight TimeSformer
- OpenCV, Albumentations
- comma.ai dataset (or similar)
- Stable-Baselines3 / custom RL
- CARLA simulator for evaluation (optional)

---

## 📁 Repository Structure
```
autonomous-driving-foundation-stack/
├── README.md
├── perception/
│   ├── datasets/
│   ├── models/
│   ├── train_perception.py
├── imitation_learning/
│   ├── models/
│   ├── train_imitation.py
├── offline_rl/
│   ├── envs/
│   ├── train_rl.py
├── data_engine/
│   ├── filtering/
│   ├── synthetic/
├── scripts/
├── configs/
├── notebooks/
└── .gitignore
```

---

## 🚀 Getting Started
```
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```
Download a driving dataset (comma.ai or open-source datasets) and update paths inside `configs/*.yaml`.

---

## 🧪 Training
### Perception
```
python perception/train_perception.py --config configs/perception.yaml
```

### Imitation Learning
```
python imitation_learning/train_imitation.py --config configs/imitation.yaml
```

### Offline RL
```
python offline_rl/train_rl.py --config configs/offline_rl.yaml
```

---

## 📊 Evaluation
- **Perception:** IoU, segmentation overlays
- **Imitation:** MSE/MAE for steering prediction
- **Offline RL:** lane departures, safety score, intervention count in simulator

---

## 🧭 Roadmap
- [x] Baseline imitation learning
- [x] Basic perception model
- [ ] Unified multi-task video backbone
- [ ] Offline RL integration
- [ ] Data engine filtering
- [ ] Synthetic rare-case augmentation
- [ ] Simulator demo and analysis

---

## 🎯 Project Motivation
This project brings together the core components of modern autonomous driving systems in a compact, research-focused format:
- Video foundation models
- Multi-task perception
- Imitation learning
- Offline reinforcement learning
- Data-centric pipelines


---

## 📬 Contact
For collaboration or feedback, feel free to reach out.
