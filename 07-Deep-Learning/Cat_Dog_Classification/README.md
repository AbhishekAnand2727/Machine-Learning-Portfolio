# Cat vs. Dog Classification: A Deep Learning Journey

## Aim of the Project

**The primary aim of this project was to successfully build and train a deep learning model to accurately classify images as either a cat or a dog.**

This project also served as a practical exploration of common challenges in computer vision, specifically:

- Dealing with overfitting in custom-built Convolutional Neural Networks (CNNs).
- Applying regularization techniques (like Dropout and Early Stopping) to improve model generalization.
- Implementing Transfer Learning with a pre-trained model (VGG16) to achieve high accuracy where the custom models failed.

---

## The Model Development Journey

The project was conducted in three distinct phases, building upon the lessons learned from the previous one.

---

### **Model 1: The Baseline Custom CNN**

This was a foundational CNN built from scratch to establish a baseline.

**Architecture:**  
A simple Sequential model with 3–4 `Conv2D` and `MaxPool2D` layers, followed by a `Flatten` layer and a `Dense` classifier.

**Result:**  
This model demonstrated severe overfitting.

- **Training Accuracy:** ~92%  
- **Validation Accuracy:** ~78%

**Conclusion:**  
The massive gap between the training and validation scores showed that the model was "memorizing" the training images and was unable to generalize to new, unseen images.

---

### **Model 2: The Regularized Custom CNN**

The goal of the second model was to combat the overfitting seen in Model 1.

**Key Changes:**

- **Dropout Layers:** Added `Dropout(0.5)` layers after the Dense layers to randomly deactivate neurons during training, forcing the network to learn more robust features.  
- **Reduced Complexity:** The number of nodes in the Dense layers was slightly reduced.  
- **Early Stopping:** An `EarlyStopping` callback was used to monitor `val_loss` and stop the training process as soon as the model stopped improving.

**Result:**  
Overfitting was successfully controlled, but the model's performance was limited.

- **Training Accuracy:** ~80%  
- **Validation Accuracy:** ~78%

**Conclusion:**  
The regularization techniques worked perfectly, bringing the training and validation scores close together. However, the peak accuracy of 78% showed the limitations of a simple, custom-built CNN for this complex task. The model was too simple to learn the intricate features of cats and dogs.

---

### **Model 3: VGG16 Transfer Learning (The Solution)**

Since our custom models hit a performance ceiling, the final approach used **Transfer Learning**.

**Method:**

1. **Load VGG16:** The VGG16 model, pre-trained on the massive ImageNet dataset, was loaded without its top classifier.  
2. **Freeze Base:** The entire convolutional base of VGG16 was "frozen" so its 138 million learned weights would not be changed.  
3. **Add New Head:** A new classifier head (identical to our custom model's) was added on top.  
4. **Data Augmentation:** An `ImageDataGenerator` was used to apply random zooms, rotations, and flips to the training images. This artificially expanded our dataset and is a crucial step in preventing overfitting.  
5. **Train the Head:** The model was trained for 30 epochs. Only the new Dense layers (our head) were trained.  
6. **Fine-Tuning:** The top convolutional block of VGG16 (`block5`) was "unfrozen". The model was then re-compiled with a very low learning rate (`1e-5`) and trained for 20 more epochs. This step fine-tunes the VGG16 features to be more specific to cats and dogs.

---

## Final Project Results

The transfer learning approach was a clear success, demonstrating a massive leap in performance.

| **Model** | **Validation Accuracy** | **Key Takeaway** |
|------------|--------------------------|------------------|
| **Model 1: Baseline CNN** | ~78% | Failed due to severe overfitting. |
| **Model 2: Regularized CNN** | ~78% | Fixed overfitting, but was too simple to learn. |
| **Model 3: VGG16 (Fine-Tuned)** | **93.5%** | Successful. Leveraged pre-trained features. |

---

### **Final Summary**

The final model achieved **93.5% validation accuracy**, proving that **transfer learning** is the correct and most powerful technique for this kind of image classification problem.
