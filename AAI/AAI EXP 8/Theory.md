
# AIM
Explore the working of a pre-trained model towards outcome generation using TensorFlow.

---

# THEORY

## What is a Pre-trained Model?
A pre-trained model is a deep learning model that has already been trained on a large dataset (such as ImageNet) and can be reused for tasks like:
- Image classification  
- Feature extraction  
- Transfer learning  

These models save time and computational resources while providing high accuracy.

---

## Selected Model: MobileNetV2

MobileNetV2 is a lightweight convolutional neural network designed for:
- Efficient performance on mobile and embedded devices  
- Faster computation with fewer parameters  
- High accuracy on image classification tasks  

It is pre-trained on the ImageNet dataset, which contains over 1 million images across 1000 classes.

---

## Working of Pre-trained Model

### 1. Input Image
- Image is resized to required dimensions (224 × 224)
- Pixel values are normalized

### 2. Feature Extraction
- Convolutional layers extract features like edges, textures, patterns

### 3. Prediction Layer
- Fully connected layers output probabilities for each class

### 4. Output Generation
- Model predicts top classes with highest probabilities

---

## Advantages of Pre-trained Models
- Reduces training time  
- Requires less data  
- High performance  
- Useful for real-world applications  

---

# PYTHON CODE

```python
import tensorflow as tf
import numpy as np
import matplotlib.pyplot as plt
from tensorflow.keras.applications import MobileNetV2
from tensorflow.keras.applications.mobilenet_v2 import preprocess_input, decode_predictions
from tensorflow.keras.preprocessing import image

# Load Pre-trained Model
model = MobileNetV2(weights='imagenet')

# Load Image
img_path = tf.keras.utils.get_file(
    'elephant.jpg',
    'https://storage.googleapis.com/download.tensorflow.org/example_images/elephant.jpg'
)

img = image.load_img(img_path, target_size=(224, 224))
img_array = image.img_to_array(img)

# Preprocess Image
img_array = np.expand_dims(img_array, axis=0)
img_array = preprocess_input(img_array)

# Prediction
predictions = model.predict(img_array)

# Decode Predictions
decoded = decode_predictions(predictions, top=3)[0]

# Display Image
plt.imshow(img)
plt.axis('off')
plt.title("Input Image")
plt.show()

# Print Predictions
print("Top Predictions:")
for i, (imagenetID, label, prob) in enumerate(decoded):
    print(f"{i+1}. {label} - {prob*100:.2f}%")
