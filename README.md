# Process Mining 2.0: Predictive Enterprise "Digital Twins"

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-ee4c2c.svg)
![PM4Py](https://img.shields.io/badge/PM4Py-Process_Mining-orange.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

## Overview
Modern enterprises operate on complex Information Systems (ERP, CRM, SCM) that generate massive, structured event logs. While traditional Process Mining excels at descriptive analytics—visualizing what went wrong in the past—it lacks the proactive capability to anticipate future bottlenecks.

This repository contains the codebase for **Process Mining 2.0**, a Bachelor Thesis project that transitions process mining into a predictive science. By adapting the architecture of Large Language Models (LLMs)—specifically Transformer Neural Networks with multi-head self-attention—this project treats sequential business event logs like natural language. The resulting model acts as a predictive "Digital Twin," forecasting the exact next activity and remaining cycle time of a live business process before an SLA violation occurs.

## Data Sources
This project relies on the open-source, globally benchmarked **BPI (Business Process Intelligence) Challenge** datasets. Due to file size constraints, the raw event logs are not hosted in this repository.

To reproduce the environment, please download the datasets directly from the 4TU.ResearchData repository and place them in the local `data/` directory:
* **[BPI Challenge 2012](https://data.4tu.nl/articles/dataset/BPI_Challenge_2012/12689204)** (13,087 traces, 262,200 events)
* **[BPI Challenge 2017](https://data.4tu.nl/articles/dataset/BPI_Challenge_2017/12696884)** (31,509 traces, 1,202,267 events)

## Project Architecture
The technical pipeline is divided into three core phases:
1.  **Event Log Tokenization:** Extraction of `.xes` logs using PM4Py, transforming discrete business activities (tasks, resources, timestamps) into dense, continuous vector embeddings.
2.  **Temporal Positional Encoding:** Injection of custom, time-aware positional encodings so the parallel Transformer architecture understands the chronological gaps between sequential events.
3.  **Multi-Task Prediction Head:** A bifurcated neural network outputting both Categorical Classification (the next predicted activity) and Temporal Regression (remaining cycle time).

## Repository Structure
```text
├── data/                  # Local directory for XES/CSV event logs (Git Ignored)
├── notebooks/             # Jupyter notebooks for Exploratory Data Analysis (EDA)
├── src/                   # Python source code for preprocessing and modeling
│   ├── preprocess.py      # XES extraction and feature embedding logic
│   ├── transformer.py     # PyTorch Transformer model architecture
│   └── evaluate.py        # PR-AUC, MAE, and RMSE evaluation metrics
├── requirements.txt       # Python dependencies
└── README.md              # Project overview and execution instructions
