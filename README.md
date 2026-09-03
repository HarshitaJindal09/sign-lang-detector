# 🤟 Sign Language Detector

A real-time American Sign Language (ASL) detection system that uses a webcam to recognize hand gestures and convert them into letters and text directly in the browser.

## 🚀 Live Demo is here 

**Try the deployed application:**

[Sign Language Translator](https://sign-language-translator-mbs7.onrender.com/)

---

## ✨ Features

* 📷 Real-time webcam-based sign language detection
* 🤟 Recognition of **28 classes** — A–Z, Nothing, and Space
* 🖐️ Hand landmark detection using MediaPipe
* 🤖 Random Forest machine learning classifier.
* ⚡ Lightweight landmark-based inference
* 📝 Automatic text generation from recognized signs
* ⏱️ Sign confirmation after holding a gesture for approximately 1 second
* 🌐 Browser-based interface
* ☁️ Deployed on Render using render website

---

## 🔍 How It Works

1. The browser accesses the user's webcam and captures frames.
2. Each frame is sent to the Flask backend as a Base64-encoded JPEG.
3. **MediaPipe Hands** detects the hand and extracts 21 hand landmarks.
4. The landmark coordinates are normalized and converted into model features.
5. A **Scikit-learn Random Forest classifier** predicts the corresponding sign.
6. The backend annotates the frame with the detected hand landmarks and prediction.
7. The processed frame and prediction are returned to the browser.
8. The detected character is added to the predicted text after the sign remains stable for approximately 1 second.

### Architecture

```text
Browser Webcam
      ↓
Base64 Image
      ↓
Flask Backend
      ↓
OpenCV
      ↓
MediaPipe Hands
      ↓
21 Hand Landmarks
      ↓
Normalized Coordinates
      ↓
Random Forest Classifier
      ↓
A–Z / Nothing / Space
      ↓
Predicted Text
```

---

## 🛠️ Tech Stack

| Layer                | Technologies                     |
| -------------------- | -------------------------------- |
| Backend              | Python, Flask, Gunicorn          |
| Hand Tracking        | MediaPipe Hands                  |
| Machine Learning     | Scikit-learn Random Forest       |
| Image Processing     | OpenCV                           |
| Numerical Processing | NumPy                            |
| Frontend             | HTML, CSS, JavaScript, Bootstrap |
| Deployment           | Render                           |

---

## 🧠 Machine Learning Model

The application uses a **Random Forest classifier** trained using hand landmark features rather than directly classifying raw images.

MediaPipe extracts **21 hand landmarks**, with each landmark containing normalized X and Y coordinates.

This produces:

```text
21 landmarks × 2 coordinates = 42 features
```

These features are passed to the trained Random Forest model to classify the gesture.

The deployed model is stored as:

```text
models/final_model.p
```

The application recognizes:

```text
A B C D E F G H I J K L M
N O P Q R S T U V W X Y Z
Nothing
Space
```

---

## 📊 Dataset

The project was trained using the **ASL Alphabet dataset** from Kaggle.

Dataset:

[ASL Alphabet — Kaggle](https://www.kaggle.com/datasets/grassknoted/asl-alphabet)

The original dataset contains images representing ASL alphabet gestures along with additional classes.

For this application, hand landmarks are extracted from the images and used as features for the classifier.

---

## 📁 Project Structure

```text
sign-lang-detector/
│
├── app.py                     # Flask application and prediction API
├── requirements.txt           # Python dependencies
├── Procfile                   # Gunicorn configuration for deployment
├── .python-version            # Python version used for deployment
│
├── models/
│   ├── final_model.p          # Trained Random Forest model
│   ├── simple-cnn.keras       # CNN model
│   └── simple-cnn2.keras      # CNN model
│
├── templates/
│   ├── index.html             # Landing page
│   └── camera.html            # Live detection page
│
├── static/
│   └── styles.css             # Frontend styling
│
├── Test/                      # Test/sample images
│
├── real-time-app.py           # Real-time application experimentation
└── model-training.ipynb       # Model training notebook
```

---

## ⚙️ Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/HarshitaJindal09/sign-lang-detector.git
cd sign-lang-detector
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Start the Flask application

```bash
python app.py
```

The application runs locally at:

```text
http://localhost:5001
```

Open the URL in your browser and allow camera access.

---

## ☁️ Deployment

The application is deployed using **Render**.

### Production server

```text
Gunicorn
```

### Start command

```bash
gunicorn app:app --timeout 120
```

### Live Application

https://sign-language-translator-mbs7.onrender.com/

---

## 🎯 Tips for Better Detection

For better recognition:

* Ensure your hand is clearly visible.
* Use good lighting.
* Keep your entire hand inside the camera frame.
* Avoid highly cluttered backgrounds.
* Keep your hand relatively steady.
* Hold a gesture for approximately **1 second** to confirm the character.
* Make sure the camera has permission to access your webcam.

---

## 🔐 Camera Access

The application uses the browser's camera permission system.

When opening the application for the first time, allow camera access when prompted.

Camera access generally requires **HTTPS or localhost**. The deployed Render application uses HTTPS, so webcam access can work directly from the browser.

---

## 🚧 Future Improvements

* Support for complete ASL words and sentences
* Improved prediction smoothing
* User-specific prediction sessions
* Confidence scores for predictions
* Support for dynamic gestures
* Mobile-friendly camera experience
* Improved handling of multiple simultaneous users
* Larger vocabulary beyond alphabet-level recognition

---

## 👩‍💻 Author

**Harshita Jindal**

### 🔗 Project Links

* **GitHub:** https://github.com/HarshitaJindal09/sign-lang-detector
* **Live Demo:** https://sign-language-translator-mbs7.onrender.com/

---

## ⭐ Project Highlights

This project demonstrates the integration of:

```text
Computer Vision
      +
Machine Learning
      +
Hand Landmark Detection
      +
Flask Backend
      +
Browser Webcam
      +
Cloud Deployment
```

The result is a complete end-to-end sign language recognition application that can be accessed through a web browser.
