# AIM
Train a **Variational Autoencoder (VAE)** using TensorFlow on the Fashion MNIST dataset.

---

# THEORY

## What is a Variational Autoencoder (VAE)?
A Variational Autoencoder (VAE) is a generative deep learning model that learns to encode input data into a **probabilistic latent space** and reconstruct it back. Unlike traditional autoencoders, VAEs learn the **distribution** of data rather than a fixed encoding.

### Key Features:
- Learns mean (μ) and variance (σ²) of latent variables
- Generates new data samples
- Uses probabilistic approach for better generalization

---

## Architecture of VAE

### 1. Encoder
- Takes input image
- Outputs:
  - Mean (μ)
  - Log variance (log σ²)

### 2. Latent Space
- Represents data as a distribution
- Sampling is done using the reparameterization trick

### 3. Decoder
- Reconstructs image from latent vector

---

## Reparameterization Trick
To enable backpropagation through randomness:

z = μ + σ * ε  
where ε ~ N(0,1)

---

## Loss Function

### 1. Reconstruction Loss
Measures how well the output matches input.

### 2. KL Divergence Loss
Ensures latent space follows normal distribution.

### Combined Loss:
L = Reconstruction Loss + KL Divergence

---

## Dataset: Fashion MNIST
- 28x28 grayscale images
- 10 clothing categories
- Used for benchmarking image models

---

## Why TensorFlow?
- Easy model building using Keras API
- Efficient computation with GPU support
- Widely used in industry and research

---

# PYTHON CODE

```python
import tensorflow as tf
from tensorflow.keras import layers, Model
import numpy as np
import matplotlib.pyplot as plt

# Load dataset
(x_train, _), (x_test, _) = tf.keras.datasets.fashion_mnist.load_data()

x_train = x_train.astype("float32") / 255.
x_test = x_test.astype("float32") / 255.

x_train = x_train.reshape(-1, 28, 28, 1)
x_test = x_test.reshape(-1, 28, 28, 1)

latent_dim = 2

# Encoder
inputs = layers.Input(shape=(28,28,1))
x = layers.Conv2D(32,3,strides=2,activation="relu",padding="same")(inputs)
x = layers.Conv2D(64,3,strides=2,activation="relu",padding="same")(x)
x = layers.Flatten()(x)
x = layers.Dense(128, activation="relu")(x)

z_mean = layers.Dense(latent_dim)(x)
z_log_var = layers.Dense(latent_dim)(x)

def sampling(args):
    z_mean, z_log_var = args
    epsilon = tf.random.normal(shape=tf.shape(z_mean))
    return z_mean + tf.exp(0.5 * z_log_var) * epsilon

z = layers.Lambda(sampling)([z_mean, z_log_var])
encoder = Model(inputs, [z_mean, z_log_var, z])

# Decoder
latent_inputs = layers.Input(shape=(latent_dim,))
x = layers.Dense(7*7*64, activation="relu")(latent_inputs)
x = layers.Reshape((7,7,64))(x)

x = layers.Conv2DTranspose(64,3,strides=2,padding="same",activation="relu")(x)
x = layers.Conv2DTranspose(32,3,strides=2,padding="same",activation="relu")(x)

outputs = layers.Conv2DTranspose(1,3,activation="sigmoid",padding="same")(x)
decoder = Model(latent_inputs, outputs)

# VAE Model
class VAE(Model):
    def __init__(self, encoder, decoder):
        super().__init__()
        self.encoder = encoder
        self.decoder = decoder

    def train_step(self, data):
        if isinstance(data, tuple):
            data = data[0]

        with tf.GradientTape() as tape:
            z_mean, z_log_var, z = self.encoder(data)
            reconstruction = self.decoder(z)

            recon_loss = tf.reduce_mean(
                tf.keras.losses.binary_crossentropy(data, reconstruction)
            ) * 28 * 28

            kl_loss = -0.5 * tf.reduce_mean(
                1 + z_log_var - tf.square(z_mean) - tf.exp(z_log_var)
            )

            total_loss = recon_loss + kl_loss

        grads = tape.gradient(total_loss, self.trainable_weights)
        self.optimizer.apply_gradients(zip(grads, self.trainable_weights))

        return {"loss": total_loss}

# Train model
vae = VAE(encoder, decoder)
vae.compile(optimizer=tf.keras.optimizers.Adam())
vae.fit(x_train, epochs=10, batch_size=128)

# Generate images
def generate():
    n = 10
    grid = np.linspace(-2, 2, n)
    canvas = np.zeros((28*n, 28*n))

    for i, yi in enumerate(grid):
        for j, xi in enumerate(grid):
            z_sample = np.array([[xi, yi]])
            img = decoder.predict(z_sample)
            canvas[i*28:(i+1)*28, j*28:(j+1)*28] = img[0].reshape(28,28)

    plt.imshow(canvas, cmap="gray")
    plt.axis("off")
    plt.show()

generate()
