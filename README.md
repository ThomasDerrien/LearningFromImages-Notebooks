## Detecting Licence Plates 
Work done by : 
* Thomas Derrien
* Arthur Mauger
* Julien Crabos

This project focuses on evaluating and comparing various **CNNs models** combined with **sequence predictors** for detecting license plates in car images. The goal is to identify the most efficient and accurate model for real-world applications, considering factors such as character accuracy, word accuracy, and model size. 

Accurate license plate detection is crucial for applications like traffic enforcement and vehicle identification, where errors can have significant consequences.

## Data Creation and Filtering

For this project, license plate images were scraped from the **PlatesMania website** using a custom-built scraper, which can be found on GitHub at [PlatesMania-Scraper](https://github.com/ThomasDerrien/PlatesMania-Scraper).

After collecting the data, we applied a filtering process to remove images from countries with special characters in their names, specifically: 
- URSS
- China
- Egypt
- Japan
- Mongolia
- Morocco
- Non Recognized
- Russia
- North Korea
- Thailand
- Saudi Arabia.

From the filtered dataset, we selected a total of **20,000 images**. These images were then split into three subsets for training, validation, and testing. 

The dataset was partitioned as follows:
- 70% for training,
- 15% for validation
- 15% for testing


## Plate Detection

#### Models Evaluated

| Model                | Feature Extractor | Sequence Predictor |
|----------------------|--------------------|---------------------|
| Resnet50-lstm        | ResNet50           | LSTM                |
| Resnet50-transfo     | ResNet50           | Transformer Encoder |
| EfficientNet-lstm    | EfficientNet-B0    | LSTM                |
| EfficientNet-transfo | EfficientNet-B0    | Transformer Encoder |
| MobileNet-lstm       | MobileNet          | LSTM                |
| MobileNet-transfo    | MobileNet          | Transformer Encoder |

#### Hyperparameters for LSTMs and Transformers

**LSTM Hyperparameters**:

| Parameter       | Value |
|-----------------|-------|
| Hidden size    | 64    |
| Number of layers| 2     |
| Dropout rate   | 0.2   |

**Transformer Encoder Hyperparameters**:

| Parameter          | Value |
|--------------------|-------|
| Transformer dimension | 64  |
| Number of heads    | 8     |
| Number of layers   | 2     |
| Dropout rate       | 0.2   |

These hyperparameters were chosen to balance model complexity and performance, ensuring efficient training and accurate predictions.

#### Preprocessing

1. **Image Extraction**: License plates are extracted from images using YOLO detections (coordinates provided in `detections.csv`).
2. **Resizing**: Extracted plates are resized to a uniform dimension (128x256 pixels).
3. **Label Encoding**: License plate labels are encoded using a character-to-index mapping.

#### Training Process

1. **Data Loading**: Images and labels are loaded using PyTorch's `Dataset` and `DataLoader`.
2. **Model Training**: Models are trained using the Adam optimizer with a learning rate of **1e-4** for LSTM-based models and **1e-3** for Transformer-based models. Early stopping is implemented to prevent overfitting.
3. **Evaluation**: Models are evaluated on a test dataset to compute character accuracy and word accuracy.

#### Results

| Model                | Char-acc | Word-acc | Size (Mega Bytes) |
|----------------------|----------|----------|--------------------|
| Resnet50-lstm        | 91.59%   | 67.78%   | 106MB              |
| Resnet50-transfo     | 88.03%   | 53.54%   | 106MB              |
| EfficientNet-lstm    | 87.85%   | 54.49%   | 23.4MB             |
|**EfficientNet-transfo**| **93.10%**   | **77.25%**   | **21.5MB**             |
| MobileNet-lstm       | 79.05%   | 30.58%   | 17.8MB             |
| MobileNet-transfo    | 86.06%   | 49.71%   | 16MB               |

#### Conclusion

EfficientNet-transfo stands out as the best model, achieving the highest word accuracy and character accuracy while maintaining a compact size.








