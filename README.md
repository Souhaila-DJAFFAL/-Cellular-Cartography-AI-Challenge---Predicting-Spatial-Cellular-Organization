# AI Challenge: Predicting Spatial Cellular Organization from Histology Images

This repository contains a Jupyter Notebook created for the [Elucidata AI Challenge 2025](https://www.kaggle.com/competitions/el-hackathon-2025), which focuses on predicting the **spatial cell-type composition** of tissue sections based on histology images (H\&E stained slides).

## 🧠 Problem Statement

The task is to **predict the relative abundance of 35 cell types** for each spot in a histological image of a tissue slide using image data alone. Each spot is approximately 55μm in diameter, and the output must be a CSV containing predictions for all spots in the test slide (`S_7`).

### 🧪 Objective

* Input: H\&E-stained image slides with spot coordinates.
* Output: Relative abundances (values between 0 and 1) of 35 predefined cell types for each spot in the test slide.

---

## 📊 Exploratory Data Analysis (EDA)

The EDA section of the notebook covers:

* **Visual inspection of training slides**: Spot locations are overlaid on histology images using red scatter points.
* **Statistical distributions** of cell-type abundances across different slides, showcasing variance and sparsity.
* **Spatial analysis** of specific cell types (e.g., C1–C3) to observe clustering or uniformity within slides.
* **Dimensionality reduction (optional)**: Techniques like PCA or t-SNE (if used) are applied to explore underlying data structure.

---

## 🧠 Modeling Approaches

The notebook includes two main modeling pipelines:

### 🔁 Submission 1: Baseline CNN Model (Patch-Based Regression)

**Pipeline**:

* Crop small patches (around each spot) from the histology images.
* Normalize and resize patches.
* Train a Convolutional Neural Network (e.g., ResNet18) using patch images as input and cell-type vectors as output.
* Use Mean Squared Error (MSE) loss for multi-output regression.
* Apply global average pooling to reduce overfitting.

**Key Features**:

* Trained on all training slides.
* Predicted for all spots in `S_7`.
* Output saved to `submission.csv`.

**Pros**:

* Interpretable and straightforward.
* Good baseline for improvement.

---

### 🎯 Submission 2: Feature Extractor + Regressor (Transfer Learning)

**Pipeline**:

* Use a pretrained CNN (e.g., EfficientNetB0) as a fixed feature extractor.
* Extract image embeddings for each patch.
* Train a lightweight regressor on extracted features.
* Normalize cell-type distributions using softmax or min-max scaling.

**Key Features**:

* Faster training.
* Incorporates pre-learned visual representations from large datasets (e.g., ImageNet).
* More flexible and modular architecture.

**Pros**:

* Leverages pretrained knowledge.
* Improves generalization on limited biomedical data.

---

## 📝 Submission Format

The final output `submission.csv` must contain:

```csv
ID,C1,C2,...,C35
S_7_0,0.001,0.002,...,0.005
...
S_7_2699,0.0005,...,0.009
```

* Each row corresponds to a spot in the test slide.
* Values represent predicted relative cell-type abundances.

---

## 📈 Evaluation Metric

Submissions are evaluated using **Spearman correlation** between predicted and actual cell-type distributions. This emphasizes rank consistency rather than absolute value accuracy.

---

## 🚀 How to Run

1. Place the `elucidata_ai_challenge_data.h5` file in the working directory or Kaggle input path.
2. Run all cells in the notebook.
3. Ensure the generated `submission.csv` follows the required format.

---

## 📚 Libraries Used

* NumPy, Pandas
* Matplotlib, Seaborn
* PyTorch / TensorFlow (depending on model)
* scikit-learn
* h5py (for reading .h5 data)

---

## 📎 Notes

* No external datasets were used (per competition rules).
* Ensure model inference runs within the 9-hour runtime limit.
* Use GPU acceleration for faster training if available.

