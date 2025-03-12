# Backdoor Detector for BadNets Using Neural Cleanse

## Overview
This project implements a robust defense mechanism against backdoor attacks in Deep Neural Networks (DNNs) using the Neural Cleanse approach. Backdoors are hidden patterns trained into DNN models that produce unexpected behavior when triggered by specific inputs, making them a significant security concern in AI systems.

## Problem Statement
DNNs are inherently black-box in nature, making them susceptible to backdoor attacks where malicious actors can embed hidden patterns that activate only when specific trigger inputs are present. For example, in a traffic sign recognition system, a specific symbol on a "Stop" sign could cause it to be misclassified as a "Yield" sign, with potentially dangerous consequences.

## Project Goals
1. **Detection**: Identify if a given DNN model (BadNet) contains backdoors by finding potential input triggers that would produce misleading classifications
2. **Mitigation**: Implement a generalized solution to mitigate the backdoor and return a "GoodNet" which reduces the effect of the backdoor

## Defense Approach
We implemented the approach specified in the Neural Cleanse paper for several reasons:
- The methods are highly generalizable, allowing us to expose an API that takes a BadNet and a validation dataset and returns a GoodNet
- The "Unlearning" model patching algorithm efficiently mitigates backdoors without significantly affecting model performance on normal inputs
- This approach avoids the drawbacks of other methods like Fine-Pruning, which can rapidly degrade model performance

## Technical Implementation

### Backdoor Detection
The detection algorithm works by:
1. For each potential target label, reverse engineering a trigger pattern and mask
2. Computing the L1 norm for each potential trigger
3. Running an outlier detection algorithm to identify the real trigger

### Backdoor Mitigation
For mitigating the backdoor, we implemented the "unlearning" approach:
- Fine-tune the model for a single epoch
- Use a small sample (10%) of the training dataset
- Add the reversed trigger to 20% of the samples without modifying labels

This approach is robust and relatively insensitive to parameters like the amount of training data and ratio of modified training data.

## Results
The implementation successfully detects and mitigates backdoor attacks in neural networks, as demonstrated by the example images of generated reverse triggers included in the repository.

## Technologies Used
- Python
- TensorFlow/Keras
- Neural Cleanse methodology

## Repository Structure
- `MLSProject.ipynb`: Main implementation notebook
- `architecture.py`: Neural network architecture definitions
- `eval.py`: Evaluation utilities
- `data/`: Dataset directory
- `models/`: Trained model files
- `results/`: Output results and visualizations

## References
This project is based on the research paper "Neural Cleanse: Identifying and Mitigating Backdoor Attacks in Neural Networks" by Wang et al.