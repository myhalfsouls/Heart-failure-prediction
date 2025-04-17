# CSE6250 Big Data for Healthcare Final Project

## Team members
Yi Zhang and Nian Liu

## Overview
The goal of this project is to reproduce the main results from the paper "Predicting Heart Failure Readmission from Clinical Notes Using Deep Learning" by Liu et al. Specifically, the original paper applies convolutional neural networks (CNNs) for natural language processing (NLP) tasks, learning from electronic health record (EHR) discharge notes related to heart failture in order to predict probability of readmission. The paper also compares results obtained from CNNs with traditional machine learning techniques such as random forests. Here, we recreate both the CNN model and the random forest model, and compare the test results against what was reported in the publication. Additionally, we also build a transformer model, which is designed specifically for NLP tasks, to explore whether prediction performance on the same task can be further improved.

## Dataset
We use the [MIMIC-III Clinical Database](https://physionet.org/content/mimiciii/1.4/) dataset for this project. Specifically, three CSV files are required: 

- ADMISSIONS.csv: contains admission and discharge times.
- DIAGNOSES_ICD.csv: contains diagnosis codes (filtered for heart failure).
- NOTEEVENTS.csv: contains dischage notes. 

After obtaining the CSV files, transfer them to the './data/' directory.

Additionally, the project also requires the word2vec embeddings pretrained on PubMed abstracts and PubMed central articles, which can be found [here](http://bio.nlplab.org/).

## Python environment
All packages are listed in requirements.txt. We used python version 3.11.4.

## Code files
All code were written in Jupyter notebooks.

- data_processing.ipynb contains code for data preprocessing. It will read the three CSV files from './data/' and write a new file 'data_processed.csv' into the same folder. 'data_processed.csv' will contain properly filtered data that are labeled positive for general readmission, labeled positive for 30-day readmission, or labeled negative for both. Each row also contains the corresponding discharge notes.

- CNN_model.ipynb contains code for applying word2vec embeddings discharge notes (from ./data/data_processed.csv), train/val/test set generation, class balancing, as well as training and testing of a CNN model. Two separate models will be trained and tested, one for the general readmission dataset and the other for the 30-day readmission dataset. Note the final model is very large and requires a lot of memory to run (~24 GB VRAM).

- RF_model.ipynb contains code for vectorizing discharge notes (from ./data/data_processed.csv) into TF-IDF vectors, train/val/test set generation, class balancing, as well as training and testing of a random forest model. Two separate models will be trained and tested, one for the general readmission dataset and the other for the 30-day readmission dataset.

- Transformer_model.ipynb contains code for tokenizing discharge notes (from ./data/data_processed.csv), train/val/test set generation, class balancing, as well as training and testing of a transformer model. Two separate models will be trained and tested, one for the general readmission dataset and the other for the 30-day readmission dataset.

## References
Liu, X., Chen, Y., Bae, J., Li, H., Johnston, J., & Sanger, T. (2019). Predicting heart failure readmission from clinical notes using deep learning. IEEE.

Johnson, A., Pollard, T., & Mark, R. (2016). MIMIC-III Clinical Database (version 1.4). PhysioNet. 

Pyysalo, S., Ginter, F., Moen, H., Salakoski, T., & Ananiadou S. (2013). Distributional semantics resources for biomedical text processing. LBM