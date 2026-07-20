# Adversarial Machine Learning — Red Team / Blue Team Security Evaluation

Built as part of the **ELE8100 CyberAI** module, MSc Applied Cybersecurity, Queen's University Belfast.

## Overview

This project conducts a full **red team / blue team security evaluation** of "FaceGuard," a CNN-based facial recognition access control system. It simulates realistic attacks that an adversary could launch against a deployed AI model, and then implements and tests a defence strategy against them — mirroring how AI systems are stress-tested in real-world security assessments.

## Project Structure

### 🔴 Red Team

**1. Model Stealing (Black-Box Attack)**
Trained a proxy CNN by querying the victim model (FaceGuard) and using its predicted labels as training data — without any access to the victim's architecture or weights. Improved the attack by using a larger query set, the full available training partition, and a stronger proxy architecture.

**2. Adversarial Attacks (White-Box Attack on Proxy Model)**
With white-box access to the proxy model, implemented two adversarial attack methods:
- **FGSM (Fast Gradient Sign Method)** —
