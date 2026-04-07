# 3D Printer Failure Detection

An intelligent system for detecting failures in additive manufacturing using computer vision and Machine Learning. This project uses a Raspberry Pi with a camera to monitor 3D printers in real-time, achieving 95% accuracy in classifying defective parts.

## 🎯 Overview

Additive manufacturing (3D printing) has become increasingly relevant for rapid prototyping across various sectors. However, failures during the printing process result in significant waste of time, material (filament), and energy. Manual failure detection is inefficient, subjective, and unsuitable for continuous monitoring.

This project presents an automated solution using Machine Learning algorithms to detect and classify 3D printer failures based on visual patterns captured during the printing process.

## 🚀 Key Features

- **Real-time Monitoring**: Continuous monitoring of 3D printing processes using Raspberry Pi
- **High Accuracy**: 95% accuracy on validation set, 97% for failure detection
- **Computer Vision**: HOG (Histogram of Oriented Gradients) for feature extraction
- **Multiple ML Models**: Comparison between SVM and Random Forest classifiers
- **Automated Classification**: Binary classification (Normal/Defective)
- **Edge Computing**: Runs efficiently on Raspberry Pi hardware

## 📊 Dataset

The project uses a custom dataset of 505 images collected from a 3D printing environment:

- **Total Images**: 505
- **Training Set**: 80% (404 images)
- **Validation Set**: 20% (101 images)
- **Classes**:
  - NoDefects (Normal): 290 images (57.4%)
  - YesDefects (Failure): 215 images (42.6%)

## 🛠️ Technology Stack

### Hardware
- **Raspberry Pi 5**: Main processing unit
- **ActionCam**: Real-time image capture from printer environment

### Software & Libraries
- **Python 3**: Core programming language
- **OpenCV**: Computer vision and image processing
- **scikit-learn**: Machine Learning models (SVM, Random Forest)
- **NumPy & Pandas**: Data manipulation and analysis
- **TensorFlow/Keras**: Deep learning (optional enhancements)

### Machine Learning
- **Feature Extraction**: HOG (Histogram of Oriented Gradients)
- **Classification Models**: 
  - Support Vector Machine (SVM)
  - Random Forest
- **Preprocessing**: Image resizing, grayscale conversion, normalization

## 📈 Results

### Model Performance
- **Overall Accuracy**: ~95% on validation set
- **Low Loss**: Indicates effective learning from training data

### Per-Class Accuracy
| Class | Accuracy | Samples |
|-------|----------|---------|
| OK (Normal) | 95% | 44 |
| FALHA (Defect) | 97% | 33 |

### Confusion Matrix
- True Positives (OK correctly identified): 42
- True Negatives (Defects correctly identified): 32
- False Positives: 2
- False Negatives: 1

## 🔄 Methodology

### 1. Image Capture & Preprocessing
- Images captured in real-time from the 3D printing environment
- Resizing to standard dimensions
- Conversion to grayscale for optimization

### 2. Feature Extraction (HOG)
- Focus on identifying and extracting shape and texture patterns
- Histogram of Oriented Gradients: Robust descriptor ideal for capturing visual anomalies in 3D printing
- Output: Each image transformed into a numerical vector of 6084 dimensions representing standardized characteristics

### 3. Supervised Classification
- **Model Comparison**: SVM vs Random Forest
- **Training**: Models trained on customized dataset with class balancing to mitigate data imbalance effects
- **Objective**: Classify each feature vector as NoDefects (ok) or YesDefects (failure)

### 4. Real-time Validation
- Efficacy of the final model validated in a real-time monitoring simulation

## 📁 Project Structure

```
3d-printer-failure-detection/
├── data/
│   ├── raw/
│   │   ├── NoDefects/
│   │   └── YesDefects/
│   └── processed/
├── models/
│   ├── svm_model.pkl
│   └── random_forest_model.pkl
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_feature_extraction.ipynb
│   ├── 03_model_training.ipynb
│   └── 04_evaluation.ipynb
├── src/
│   ├── preprocessing.py
│   ├── feature_extraction.py
│   ├── training.py
│   └── inference.py
├── requirements.txt
├── README.md
└── LICENSE
```

## 🚀 Getting Started

### Prerequisites
- Python 3.7 or higher
- Raspberry Pi 5 (or compatible system)
- Camera module (ActionCam or similar)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/Wartronick/3d-printer-failure-detection.git
cd 3d-printer-failure-detection
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Download the pre-trained models:
```bash
# Models are included in the models/ directory
```

### Usage

#### Training a Model
```python
from src.training import train_model
from src.preprocessing import load_dataset

# Load dataset
X_train, X_test, y_train, y_test = load_dataset('data/processed/')

# Train model
model = train_model(X_train, y_train, model_type='svm')

# Evaluate
accuracy = model.score(X_test, y_test)
print(f"Model Accuracy: {accuracy:.2%}")
```

#### Real-time Inference
```python
from src.inference import predict_failure
import cv2

# Capture frame from camera
cap = cv2.VideoCapture(0)
ret, frame = cap.read()

# Predict
prediction = predict_failure(frame)
print(f"Status: {'NORMAL' if prediction == 0 else 'FAILURE DETECTED'}")
```

## 📊 Model Comparison

| Aspect | SVM | Random Forest |
|--------|-----|---------------|
| Accuracy | 95% | 94% |
| Training Time | Fast | Moderate |
| Interpretability | Low | High |
| Robustness | Good | Excellent |

## 🔍 Key Insights

1. **High Accuracy**: The model achieves 95% accuracy, indicating effective learning from the data
2. **Low Overfitting**: Minimal difference between training and validation curves suggests good generalization
3. **Balanced Performance**: Both classes (OK and Failure) are detected with high accuracy
4. **Practical Applicability**: Results validate the efficacy of the model for real-time monitoring scenarios

## 🎓 Academic Context

- **Institution**: UTFPR (Universidade Tecnológica Federal do Paraná)
- **Program**: Graduate Program in Electrical Engineering and Industrial Informatics
- **Advisor**: Dr. André E. Lazzaretti
- **Author**: Alexandre Domingues (MSc.)
- **Year**: 2025

## 🔮 Future Improvements

- [ ] Deep Learning models (CNN) for enhanced feature extraction
- [ ] Real-time video stream processing
- [ ] Web dashboard for monitoring
- [ ] Multi-class classification (different types of failures)
- [ ] Integration with printer APIs for automated alerts
- [ ] Mobile app for remote monitoring

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Contact

- **Author**: Alexandre Domingues
- **GitHub**: [@Wartronick](https://github.com/Wartronick)
- **Email**: [alexandre.mecatronica@hotmail.com]

## 🙏 Acknowledgments

- UTFPR and LARA Laboratory for providing resources and support
- Dr. André E. Lazzaretti for guidance and mentorship
- The open-source ML community for excellent tools and libraries

---

**Last Updated**: 2025

