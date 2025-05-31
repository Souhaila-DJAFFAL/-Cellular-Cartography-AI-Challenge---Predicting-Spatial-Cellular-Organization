🔬 **Cellular Cartography: AI Challenge - Predicting Spatial Cellular Organization**

This repository documents our approach to the AI Challenge - Prediction of Spatial Cellular Organization from Histology Images. 
Ranked: 127 from 355 teams.
The core mission is to predict the spatial abundance of 35 cell types within tissue slices using only standard Hematoxylin and Eosin (HE) stained images, bridging traditional histology with machine learning.

🗺️ **Exploratory Data Analysis (EDA)**

We began by visualizing the HE images and overlaying spot coordinates to understand the spatial relationships in both training and test datasets. 
This included examining spot tables containing coordinates and cell type annotations.

🚀 **Submissions**

Submission 1: Random Baseline

Our initial attempt established a baseline by generating random abundance predictions for all 35 cell types for each spot on the test slide. 
This provided a starting point for evaluating more complex models.

Submission 2: Neural Network-Powered Predictions 

This submission utilizes a Convolutional Neural Network (CNN), specifically leveraging a pre-trained EfficientNetB0 model.
Process: Image patches (64x64) were extracted around each spot, augmented, and used to train the CNN to predict normalized cell type abundances. 
The model was trained with MSE loss, Adam optimizer, and callbacks for early stopping and learning rate reduction.
Predictions on the test set were then de-normalized to generate the final submission file.
