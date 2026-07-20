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
- **FGSM (Fast Gradient Sign Method)** — a one-step attack that perturbs input images in the direction of the loss gradient
- **PGD (Projected Gradient Descent)** — a stronger, iterative attack that applies multiple gradient-based updates within an epsilon-bounded region

Both attacks were evaluated across a range of epsilon (perturbation strength) values, and a **targeted impersonation attack** was performed to force the model to misclassify an unauthorised individual as an authorised user (CEO, ID = 0).

**3. Transferability Attack**
Tested whether adversarial examples crafted on the proxy model would also fool the original victim model — simulating a realistic black-box scenario where the attacker never has direct access to the victim's gradients. Measured the transfer success rate for both untargeted and targeted attacks.

### 🔵 Blue Team

**4. Adversarial Training Defence**
Designed a defence strategy to improve the victim model's robustness:
- Started from the pretrained FaceGuard model
- Froze the convolutional feature extractor and BatchNorm statistics
- Fine-tuned only the classifier layers
- Trained on a mix of clean and FGSM-adversarial examples

## Key Results

| Metric | Result |
|---|---|
| Proxy model accuracy (post-improvement) | Significantly improved via larger query set + stronger architecture |
| FGSM attack effectiveness | Model accuracy dropped to ~1% for epsilon > 0.05 |
| PGD attack effectiveness | Model accuracy dropped to 0% at higher epsilon values (stronger than FGSM) |
| Adversarial training defence | Improved robustness against FGSM while preserving clean accuracy; **PGD attacks still succeeded**, showing partial defence effectiveness |

## Key Takeaways

- Both FGSM and PGD are highly effective against undefended CNN models, with PGD consistently outperforming FGSM due to its iterative nature.
- Adversarial examples transfer between models, meaning attackers don't need white-box access to the actual deployed system to compromise it.
- Adversarial training provides meaningful but **partial** protection — it hardened the model against FGSM but did not fully defend against the stronger PGD attack, highlighting the ongoing challenge of building robust ML security defences.

## Tech Stack

- **Language:** Python
- **Framework:** PyTorch
- **Techniques:** Convolutional Neural Networks (CNN), Model Extraction, FGSM, PGD, Adversarial Training

## Author

Chandana Saligrama Perumal


