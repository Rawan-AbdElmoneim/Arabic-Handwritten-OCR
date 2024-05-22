# Introduction
This article details a comprehensive project aimed at developing an Optical Character Recognition (OCR) system for converting Arabic handwritten text to digital text. The OCR system leverages a meticulously compiled dataset, the Arabic Handwritten Alphabets and Words Dataset (AHAWP), which includes a diverse collection of handwritten Arabic alphabets and words. The project's goal is to enhance the accuracy and reliability of handwriting recognition for the Arabic language, facilitating applications in various domains such as document digitization, automated data entry, and historical document preservation. This document outlines the dataset creation, preprocessing steps, and methodologies employed to develop a robust OCR system.


# Dataset Overview
## Arabic Alphabets:
The dataset covers a wide range of Arabic alphabets, including variations such as beginning, end, middle, and regular forms. This ensures comprehensive coverage of all possible character positions within words, which is crucial for accurate recognition and interpretation of handwritten Arabic text.

## Arabic Words:
The dataset contains a diverse set of Arabic words, carefully selected to represent all Arabic alphabets comprehensively. The words are chosen to include different letter combinations and contextual usages, providing a robust training ground for the OCR system.

![1081_001](https://github.com/Rawan-AbdElmoneim/Rawan-AbdElmoneim/assets/142115846/289961b7-25a6-4a86-8c5e-812885398cdf)



## Khatt Dataset:
In addition to the AHAWP dataset, the project also incorporates the Khatt dataset. The Khatt dataset is a well-known resource for Arabic handwriting recognition, comprising thousands of handwritten samples collected from various writers. This dataset adds further diversity and volume to the training data, enhancing the OCR system's ability to generalize across different handwriting styles and variations.

# Preprocessing
## Grayscale Conversion:
The input images, originally in RGB format, are first converted to grayscale. This reduces the computational complexity and focuses the model on the text's structural features rather than color information.

## Noise Removal:
To improve the quality of the input images, noise removal techniques are applied. This step helps in eliminating unwanted artifacts and background noise, ensuring that the handwritten text is more clearly defined for the OCR system.

## Cropping:
The images are cropped to isolate just the written word, removing unnecessary background. This step ensures that the focus remains on the text itself, which is crucial for accurate recognition.

## Image Resizing:
The images are resized to a consistent dimension, typically 128x128 pixels. This standardization facilitates uniform input to the neural network, aiding in efficient processing and learning.

## Normalization:
Normalization is performed to scale the pixel values to a range between 0 and 1. This step is crucial for the neural network to process the images effectively, as it ensures that the pixel intensity values are in a suitable range for the model to learn from.

## Data Augmentation
To enhance the robustness and generalization capabilities of the OCR system, data augmentation techniques are employed. These include various transformations such as rotation, scaling, and translation applied to the images, simulating different handwriting styles and conditions. This helps in creating a more diverse training set, enabling the model to perform better on unseen data.

## randomly selected data after noise removal and grayscale conversion
![Screenshot 2024-05-22 121233](https://github.com/Rawan-AbdElmoneim/Rawan-AbdElmoneim/assets/142115846/155ae39a-b59b-4950-95b7-290ca58d6d4e)

## randomly selected data after all the preprocessing process
![Screenshot 2024-05-22 121316](https://github.com/Rawan-AbdElmoneim/Rawan-AbdElmoneim/assets/142115846/bd9c44c3-4d7a-4b82-836e-a6517c881477)


# Train-Test Split and Data Merging
## Data Splitting:
We applied the train_test_split function to three different folders containing image data, splitting each folder's data into training and testing sets with a ratio of 80:20. The folders included:

Alphabets Data: This folder contained images of handwritten alphabets.
Preprocessed Words Data: This folder contained images of preprocessed handwritten words.
KHATT Data: This folder contained images from the KHATT dataset.
## Data Merging:
After splitting the data, we merged the training data of the three folders to create the final training dataset. Similarly, we merged the testing data of the three folders to create the final testing dataset. This approach ensured that our model was trained and evaluated on a diverse set of data, encompassing different writing styles and variations present in the three datasets.

# Model Architecture
The OCR system is built using a Convolutional Neural Network (CNN) combined with a Recurrent Neural Network (RNN). The CNN layers are responsible for extracting spatial features from the input images, while the RNN layers, specifically a Bidirectional LSTM, capture the sequential nature of the text. This combination allows the model to understand both the visual and contextual aspects of handwritten Arabic script.

# Importance of LSTM in OCR Systems
LSTMs, or Long Short-Term Memory networks, are a type of recurrent neural network specifically designed for processing sequences of data while addressing the vanishing gradient problem. In OCR systems, LSTMs play a crucial role by capturing long-range dependencies in handwritten text, which is essential for accurate character and word recognition. Their ability to retain context over extended sequences is particularly beneficial in interpreting the order and context of characters in handwritten scripts. In our OCR system, Bidirectional LSTM layers enhance this capability by allowing the model to understand text from both directions, contributing to more accurate decoding of handwritten Arabic text.
![figure1-4ee485edcb5d51bbed8e4fa14d54a649](https://github.com/Rawan-AbdElmoneim/Rawan-AbdElmoneim/assets/142115846/9165ba05-fc4a-42bf-b961-b9d38590be0b)


## Improved CNN-RNN Model with Bidirectional LSTM:
- **Convolutional Layers:**
  - **Conv2D Layer 1:** 32 filters, kernel size (3, 3), activation 'relu'
  - **Conv2D Layer 2:** 64 filters, kernel size (3, 3), activation 'relu'

- **MaxPooling Layers:**
  - **MaxPooling Layer 1:** Pool size (2, 2)
  - **MaxPooling Layer 2:** Pool size (2, 2)

- **Flatten Layer:** Flattens the feature maps into a single vector.

- **Dense Layer:** Fully connected layer with 128 units, activation 'relu'.

- **Reshape Layer:** Reshapes the vector to (1, 128) to add the time dimension for LSTM.

- **Bidirectional LSTM:** 128 units, return_sequences=True, captures the sequential nature of the text from both directions.

- **Output Layer:** Dense layer with softmax activation to classify the characters, with the number of units equal to the number of classes in the dataset (num_classes).

![Screenshot 2024-05-22 124148](https://github.com/Rawan-AbdElmoneim/Rawan-AbdElmoneim/assets/142115846/4da356c2-7c3c-4940-8194-083e849eaeef)

This structure enables the model to effectively extract and interpret both spatial and sequential features from the input images, leading to accurate recognition of Arabic handwritten text.


