# 🚗 Parking Spot Detection

Automatic detection of **free and occupied parking spaces** from an aerial parking image using two complementary approaches:

* 🖼️ **Traditional image processing** with OpenCV
* 🧠 **Deep Learning** using a Convolutional Neural Network (CNN)

The objective of this project is to implement and compare both approaches in terms of robustness, complexity, and confidence estimation.

---

## 📌 Project Overview

The system analyzes an aerial image of a parking lot and determines whether each predefined parking space is:

* 🟢 **Empty**
* 🔴 **Occupied**

Two different approaches are implemented and compared.

| Approach    | Method                            | Training Required | Confidence Score |
| ----------- | --------------------------------- | ----------------: | ---------------: |
| Traditional | Image processing + pixel counting |              ❌ No |             ❌ No |
| CNN         | Deep Learning classification      |             ✅ Yes |            ✅ Yes |

The parking spaces are manually defined using OpenCV's `cv2.selectROIs` tool. The input image is resized to **1280 × 720 pixels** before processing.

---

## 🗂️ Project Structure

```text
Parking-spot-detection/
│
├── CNN/
│   └── cnn_parking_detection.ipynb
│
├── Traditionnel/
│   └── parking-spot-detection.ipynb
│
├── rapport_projet.pdf
│
└── README.md
```

---

## 🖼️ 1. Traditional Image Processing

The traditional approach uses a sequence of image-processing operations to determine whether a parking spot is occupied.

### Pipeline

```text
Input Image
     │
     ▼
Grayscale Conversion
     │
     ▼
Gaussian Blur (5×5)
     │
     ▼
Adaptive Thresholding
     │
     ▼
Parking Spot ROI
     │
     ▼
White Pixel Counting
     │
     ▼
Free / Occupied
```

### Main Steps

1. Convert the image to **grayscale**.
2. Apply a **5×5 Gaussian blur** to reduce noise.
3. Apply **adaptive thresholding** to handle lighting variations.
4. Count the number of white pixels inside each parking-space ROI.
5. Use a threshold of **500 pixels** to classify the space.

```text
countNonZero(ROI) < 500 → 🟢 Free
countNonZero(ROI) ≥ 500 → 🔴 Occupied
```

This approach is simple and does not require a training dataset.

---

## 🧠 2. CNN — Deep Learning Approach

The second approach uses a **Convolutional Neural Network** trained on labeled parking-space images.

The dataset is organized into two classes:

```text
empty/
parked/
```

### CNN Architecture

```text
Input Image
    │
    ▼
Convolution 3×3
32 Filters + ReLU
    │
    ▼
Max Pooling 2×2
    │
    ▼
Flatten
    │
    ▼
Fully Connected
128 Neurons + ReLU
    │
    ▼
Fully Connected
    │
    ▼
Softmax
    │
    ├── p_empty
    └── p_parked
```

The architecture uses convolution to extract visual features, followed by fully connected layers for classification.

---

## 🔍 CNN Prediction Pipeline

For every manually defined parking-space ROI:

1. Crop the parking-space region.
2. Resize it to **64 × 64 pixels**.
3. Normalize pixel values between **0 and 1**.
4. Pass the image through the trained CNN.
5. Obtain the Softmax probabilities.
6. Display the predicted status and confidence percentage.

Example:

```text
Parking Spot #12

Status: EMPTY
Confidence: 94.7%
```

---

## 📊 Results

The two approaches were tested on the same parking image.

| Approach                     | Free Spots | Occupied Spots |
| ---------------------------- | ---------: | -------------: |
| Traditional Image Processing |          2 |             31 |
| CNN                          |          3 |             30 |

The CNN provides better robustness and additionally provides a **confidence score** for each prediction.

The traditional method remains useful as a fast baseline because it does not require a dataset or model training.

---

## ⚖️ Comparison

| Criterion           | Traditional Method              | CNN                    |
| ------------------- | ------------------------------- | ---------------------- |
| Approach            | White pixel counting            | Machine Learning       |
| Preprocessing       | Grayscale → Blur → Thresholding | Resize → Normalization |
| Training            | ❌                               | ✅                      |
| Dataset             | ❌                               | ✅                      |
| Lighting robustness | Medium                          | Good                   |
| Confidence score    | ❌                               | ✅ Softmax              |
| Complexity          | Low                             | Higher                 |
| Adaptability        | Limited                         | Better                 |

---

## 🛠️ Technologies

* **Python**
* **OpenCV**
* **TensorFlow**
* **Keras**
* **NumPy**
* **Jupyter Notebook**

The project report specifies Python, OpenCV, and TensorFlow/Keras as the main technologies used.

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Saadiaboussiar/Parking-spot-detection.git
cd Parking-spot-detection
```

### 2. Install dependencies

```bash
pip install opencv-python tensorflow keras numpy jupyter
```

### 3. Run the notebooks

Launch Jupyter:

```bash
jupyter notebook
```

Then open either:

```text
CNN/cnn_parking_detection.ipynb
```

or:

```text
Traditionnel/parking-spot-detection.ipynb
```

---

## 📈 Possible Improvements

Several improvements can make the system more robust:

* 📚 Train the CNN on a **larger dataset**
* 🧠 Add more convolutional layers
* 🔄 Use **transfer learning**
* 🌦️ Include images under different lighting and weather conditions
* 📊 Evaluate the model using accuracy, precision, recall, and F1-score
* 🚘 Test the system on multiple parking lots and different camera angles

These improvements are also suggested in the project report, particularly using a larger dataset, deeper CNN architectures, and transfer learning.

---

## 👩‍💻 Author

**Saadia Boussiar**

Engineering Student — Data Science, Big Data & Artificial Intelligence

**Project:** Parking Spot Detection
**Technologies:** Python · OpenCV · TensorFlow/Keras
---

⭐ **If you find this project useful, feel free to star the repository!**
