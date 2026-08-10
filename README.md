# 🖐️ Sign Language Recognition System

![Sign Language Recognition](https://github.com/paradise2580/Signapse--SignLanguage_Recommendation_System/blob/main/asl_sign.png)

## 📚 Project Overview

Sign Language Recognition System aims to bridge the communication gap between speech-impaired or deaf individuals and those who do not understand sign language. This system recognizes hand signs and gestures, converting them into readable text to facilitate communication.

## ✨ Features

- **Sign Language Interpreter/Translator:** Facilitates communication between deaf-dumb and normal individuals without needing a human translator.
- **Sign Language Learning Tool:** Assists in teaching sign language to deaf-dumb children.
- **Human-Computer Interface:** Allows deaf-dumb individuals to interact with computer systems.
- **Interfacing in Virtual Environment:** Uses gestures to control various systems, including computers, music systems, virtual games, home appliances, and medical equipment.

## 📊 Dataset

We are using the “Sign Language MNIST” dataset, a public-domain, free-to-use dataset available on [Kaggle](https://www.kaggle.com/datasets/datamunge/sign-language-mnist). This dataset contains pixel information for around 1,000 images of each of 24 ASL letters, excluding J and Z.

## 🚧 Challenges

- **Real-Time Recognition:** The system needs to work in uncontrolled real-time environments, coping with messy backgrounds, moving objects, diverse lighting conditions, and various users.
- **Indian Sign Language Dataset:** There's a lack of standard datasets for Indian Sign Language (ISL) and issues with standardization.
- **Dynamic Gestures:** Recognizing dynamic hand gestures and differentiating between gestures with similar meanings remains challenging.
- **False Gestures:** Detecting false gestures, such as unwanted gestures between words in a sentence, is still a challenge.
- **Two-Hand Gestures:** Many ISL alphabets use two hands, making recognition difficult.

## 🏛️ System Architecture

![Sign Language Recognition](https://github.com/paradise2580/Signapse--SignLanguage_Recommendation_System/blob/main/Architecture.png)

### 1. Data Acquisition
- **Dataset:** Sign Language MNIST dataset from [Kaggle](https://www.kaggle.com/datasets/datamunge/sign-language-mnist)
- **Format:** CSV file containing pixel information for images of ASL letters

### 2. Preprocessing
- **Image Processing:**
  - Resize images to the required input shape for the neural network
  - Normalize pixel values
  - Data augmentation using `ImageDataGenerator` to enhance training

### 3. Model Architecture
- **Sequential Model:** Using Keras
  - **Convolutional Layers:** To extract features from images
    ```python
    model.add(Conv2D(filters=32, kernel_size=(3,3), activation='relu', input_shape=(28,28,1)))
    model.add(MaxPool2D(pool_size=(2,2)))
    model.add(BatchNormalization())
    ```
  - **Fully Connected Layers:** For classification
    ```python
    model.add(Flatten())
    model.add(Dense(128, activation='relu'))
    model.add(Dropout(0.5))
    model.add(Dense(24, activation='softmax'))  # 24 classes for ASL letters
    ```
  - **Optimization and Compilation:**
    ```python
    model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
    ```

### 4. Training
- **Callbacks:** Use `ReduceLROnPlateau` to adjust learning rate during training
- **Training the Model:** Fit the model on the training data using the preprocessed and augmented images

### 5. Prediction
- **Model Inference:**
  - Load the pre-trained model using `load_model()`
  - Preprocess input images in real-time using OpenCV and Mediapipe for hand tracking
  - Predict the sign language gesture
    ```python
    model = load_model('path_to_model.h5')
    predictions = model.predict(processed_image)
    ```

### 6. Output
- **Text-to-Speech:** Convert recognized text to speech using `gTTS`
  ```python
  tts = gTTS(text=recognized_text, lang='en')
  tts.save('output.mp3')
  os.system('mpg321 output.mp3')
  ```

### 7. User Interface
- **Real-Time Recognition:** Use OpenCV to capture video frames and process them
- **Hand Tracking:** Use Mediapipe to detect hand landmarks and extract the region of interest
- **Display:** Show the recognized sign and corresponding text on the screen

### 8. Environment Setup
- **Suppress TensorFlow Warnings:**
  ```python
  os.environ['TF_CPP_MIN_LOG_LEVEL'] = '3'
  ```

## 🛠️ Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/Sign-Language-Recognition-System.git
   cd Sign-Language-Recognition-System
   ```

2. Install the required dependencies:
   ```bash
   pip install keras
   pip install pandas
   pip install gTTS
   pip install opencv-python
   pip install mediapipe
   pip install numpy

   ```

3. Run the prediction script:
   ```bash
   python prediction.py
   ```

## 🚀 Usage

1. Load the dataset:
   - Ensure the `sign_mnist_train.csv` file is in the project directory.
   
2. Train the model (details can be found in the provided documentation).

3. Use the trained model to recognize sign language gestures through the `prediction.py` script.

## 🤝 Contributing

Contributions are welcome to this project. To contribute:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -m 'Add some feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request.

  ## 👤 Author
- **Anshivya Nagpal**
