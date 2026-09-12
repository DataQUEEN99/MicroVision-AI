# MicroVision AI  
## Explainable CNN-Based Microplastic Classification Using Microscopic Images

MicroVision AI is an end-to-end computer vision project that uses Convolutional Neural Networks and transfer learning to classify microscopic images of microplastic particles. The project includes dataset preparation, exploratory data analysis, image preprocessing, CNN training, fine-tuning, performance evaluation and Grad-CAM explainability.

> **Note:** This project is intended for educational and research prototyping. It is not a certified environmental measurement or laboratory diagnostic system.

---

## Project Overview

Microplastics are small plastic particles that can be found in water, soil and marine environments. Manual identification through microscopy can be time-consuming and difficult.

This project develops an AI-based image classification pipeline that predicts the category of a microscopic particle from an input image.

The model learns visual patterns such as:

- Particle shape
- Texture
- Color
- Surface structure
- Microscopic appearance

The project also uses Grad-CAM to visualize the image regions that influenced the model’s prediction.

---

## Project Objectives

1. Load and analyze the microplastic image dataset.
2. Detect the available image classes automatically.
3. Visualize class distribution and sample images.
4. Preprocess microscopic images for CNN training.
5. Train a transfer-learning CNN using MobileNetV2.
6. Fine-tune the final layers of the pretrained network.
7. Evaluate the model using multiple classification metrics.
8. Generate a confusion matrix and class-wise accuracy chart.
9. Use Grad-CAM for explainable AI.
10. Save the trained model and evaluation results.

---

## End-to-End Pipeline

```text
Microplastic ZIP Dataset
          ↓
Dataset Upload
          ↓
ZIP Extraction
          ↓
Automatic Class Detection
          ↓
Dataset DataFrame Creation
          ↓
Exploratory Data Analysis
          ↓
Class Distribution Visualization
          ↓
Train / Validation / Test Split
          ↓
Image Resizing and Normalization
          ↓
Data Augmentation
          ↓
MobileNetV2 Transfer Learning
          ↓
CNN Classification Head
          ↓
Initial Model Training
          ↓
Fine-Tuning
          ↓
Training Curves
          ↓
Test Evaluation
          ↓
Classification Report
          ↓
Confusion Matrix
          ↓
Class-Wise Accuracy
          ↓
Grad-CAM Explainability
          ↓
Single Image Prediction
          ↓
Model and Metrics Export
```

---

## Dataset

The project uses the uploaded microplastic image dataset:

`dataset_microplastics-master.zip`

The code automatically extracts the ZIP file and detects image classes from the folder structure.

Example class names may include:

```text
PE
PHA
PS
Mixed
None
Dust
```

The exact class names depend on the folders available in the uploaded dataset.

### Dataset preparation

The code performs the following operations:

- Extracts the ZIP file.
- Finds supported image files.
- Detects class folders.
- Removes folders containing insufficient images.
- Creates a structured DataFrame.
- Converts class names into numeric labels.

Supported image formats:

```text
.jpg
.jpeg
.png
.bmp
.tif
.tiff
```

---

## Technologies Used

- Python
- TensorFlow
- Keras
- MobileNetV2
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- Google Colab
- Grad-CAM
- Transfer learning

---

## Model Architecture

The project uses MobileNetV2 pretrained on ImageNet as the feature extractor.

```text
Input Image: 224 × 224 × 3
          ↓
MobileNetV2 Backbone
          ↓
Global Average Pooling
          ↓
Batch Normalization
          ↓
Dropout
          ↓
Dense Layer: 128 Neurons
          ↓
Dropout
          ↓
Softmax Classification Layer
          ↓
Microplastic Class Prediction
```

### Why MobileNetV2?

MobileNetV2 is useful because it:

- Has a relatively lightweight architecture.
- Trains faster than many large CNNs.
- Works well with transfer learning.
- Is suitable for limited computational resources.
- Can be adapted for deployment in lightweight applications.

---

## Data Preprocessing

Each image is:

1. Loaded from disk.
2. Resized to `224 × 224` pixels.
3. Converted to RGB.
4. Converted into a TensorFlow tensor.
5. Normalized using MobileNetV2 preprocessing.
6. Augmented during training.

### Data augmentation

The training pipeline applies:

- Horizontal flipping
- Vertical flipping
- Random rotation
- Random zoom
- Random contrast adjustment

Data augmentation helps the model become more robust to changes in particle orientation, scale and appearance.

---

## Dataset Split

The dataset is divided into three subsets:

| Subset | Percentage |
|---|---:|
| Training | 70% |
| Validation | 15% |
| Testing | 15% |

A stratified split is used so that the class distribution remains approximately balanced across the subsets.

---

## Training Strategy

### Stage 1: Transfer learning

The pretrained MobileNetV2 backbone is frozen. Only the newly added classification layers are trained.

This allows the model to learn the microplastic classes without immediately modifying the pretrained feature extractor.

### Stage 2: Fine-tuning

The final layers of MobileNetV2 are unfrozen and trained with a smaller learning rate.

This allows the network to adapt its visual features to microscopic particle images.

### Training callbacks

The project uses:

- Early stopping
- Learning-rate reduction
- Best-model checkpointing

These callbacks help reduce overfitting and save the best-performing model.

---

## Exploratory Data Analysis

The project generates:

### 1. Class distribution chart

Shows the number of images available in each class.

### 2. Sample image grid

Displays representative microscopic images from the dataset.

### 3. Training and validation curves

Shows:

- Training accuracy
- Validation accuracy
- Training loss
- Validation loss

These plots help identify:

- Underfitting
- Overfitting
- Training instability
- Improvement during fine-tuning

---

## Evaluation Metrics

The trained CNN is evaluated on the unseen test dataset.

The project calculates:

- Test loss
- Test accuracy
- Precision
- Recall
- F1-score
- Classification report
- Confusion matrix
- Class-wise accuracy

### Accuracy

Accuracy measures the percentage of correctly classified images.

### Precision

Precision measures how many images predicted as a particular class actually belong to that class.

### Recall

Recall measures how many images belonging to a class were correctly detected.

### F1-score

F1-score combines precision and recall into a single metric.

---

## Confusion Matrix

The confusion matrix shows the relationship between:

- Actual classes
- Predicted classes

It helps identify which microplastic categories are commonly confused with one another.

For example, visually similar particle categories may be misclassified because of:

- Similar color
- Similar shape
- Low image resolution
- Unequal class sizes
- Overlapping microscopic characteristics

---

## Explainable AI with Grad-CAM

Grad-CAM, or Gradient-weighted Class Activation Mapping, is used to explain CNN predictions.

The Grad-CAM pipeline:

```text
Input Image
     ↓
CNN Prediction
     ↓
Gradient Calculation
     ↓
Feature Map Weighting
     ↓
Heatmap Generation
     ↓
Heatmap Overlay on Original Image
```

The heatmap highlights image regions that contributed most strongly to the predicted class.

This is useful for understanding whether the model is focusing on:

- The particle itself
- Particle edges
- Texture
- Brightness patterns
- Background artifacts

Grad-CAM improves interpretability but does not guarantee that the model’s reasoning is scientifically correct.

---

## Example Prediction Output

For an input microscopic image, the model returns:

```text
Predicted class: PE
Confidence: 92.40%
```

It also displays a probability table:

| Class | Probability |
|---|---:|
| PE | 92.40% |
| PS | 4.10% |
| PHA | 2.30% |
| Mixed | 1.20% |

The actual probabilities depend on the trained model and test image.

---

## Project Directory

After execution, the project creates the following structure:

```text
MicroVision_AI/
│
├── dataset/
│   └── Extracted dataset files
│
├── models/
│   ├── microvision_best.keras
│   ├── MicroVision_Final_CNN.keras
│   ├── class_names.json
│   └── evaluation_metrics.json
│
└── Generated plots and analysis outputs
```

---

## Saved Files

### `MicroVision_Final_CNN.keras`

The final trained CNN model.

### `microvision_best.keras`

The best checkpoint selected according to validation performance.

### `class_names.json`

Stores the class names used by the model.

### `evaluation_metrics.json`

Stores:

- Test accuracy
- Test loss
- Precision
- Recall
- F1-score
- Class names
- Dataset split sizes

---

## How to Run

### Option 1: Google Colab

1. Open Google Colab.
2. Create a new notebook.
3. Paste the complete code into one cell.
4. Run the cell.
5. Upload:

```text
dataset_microplastics-master.zip
```

6. Wait for extraction, training and evaluation to finish.
7. Review the plots and metrics.

### Install required packages

```bash
pip install tensorflow numpy pandas matplotlib seaborn scikit-learn
```

Google Colab generally already includes most of these packages.

---

## Hardware Recommendation

Recommended environment:

- Google Colab GPU
- NVIDIA T4 GPU
- At least 8 GB RAM
- Approximately 2–5 GB free storage

The dataset is small enough to run on a normal computer, but GPU training will be faster.

---

## Limitations

This project has several limitations:

- The dataset may contain a limited number of images.
- Some classes may be visually similar.
- The dataset may be imbalanced.
- Synthetic or laboratory images may not represent real environmental conditions.
- Model predictions depend on image quality.
- High confidence does not always mean correct classification.
- The model should not be used as a replacement for laboratory confirmation.

---

## Future Improvements

Possible extensions include:

1. Add more microplastic datasets.
2. Use EfficientNetB0 or ConvNeXt.
3. Apply class-weighted training.
4. Add image segmentation.
5. Detect multiple particles in one image.
6. Use YOLO for particle detection.
7. Estimate particle size and shape.
8. Add Fourier-transform features.
9. Build a Streamlit web application.
10. Deploy the model as an API.
11. Add uncertainty estimation.
12. Use ensemble CNN models.
13. Train with microscope images from different laboratories.
14. Add a pollution-density estimation module.
15. Create a complete environmental monitoring dashboard.

---

## Final Project Statement

MicroVision AI demonstrates how deep learning can be applied to microscopic image analysis for microplastic classification. By combining transfer learning, CNN-based prediction, statistical evaluation and Grad-CAM explainability, the project provides a complete computer vision workflow from raw dataset to interpretable prediction.

### Resume Description

> Developed MicroVision AI, an explainable CNN-based microplastic classification system using MobileNetV2 transfer learning. Implemented automated dataset extraction, exploratory data analysis, stratified data splitting, augmentation, fine-tuning, classification metrics, confusion matrix analysis and Grad-CAM visual explanations.

### Suggested GitHub Repository Name

```text
microvision-ai-microplastic-classification
```

### Suggested Short Description

> An explainable deep-learning system for classifying microscopic microplastic images using CNN transfer learning, performance analytics and Grad-CAM visualization.
