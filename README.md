# Palm Vein Recognition using CNNs

# Why Identify Veins in the first place?

- There are many unique human traits that have been used for biometric purposes.
- Face, iris, fingerprint, voice, and gait are examples.

> Palm-veins are a novel biometric which means they have inbuilt anti-spoofing qualities and high stability, making it impossible to fake. Additionally, veins cannot be read from lifeless bodies or severed hands.
> 

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled.png)

- And imagery is not occluded by makeup or accessories.
- Our objective is to combined three CNN models using Decision-Level Fusion to obtain a robust and highly accurate ensemble CNN system that can accurately perform palm-vein recognition.

# Dataset

Three different datasets were used to train and test the proposed architecture.

### VERA PalmVein Database

- VERA consists of 2,200 images from 110 different subjects, from 2 sessions.

![VERA Sample Image](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%201.png)

VERA Sample Image

### **FYO Database**

- FYO Database contains palmar, dorsal, and wrist vein samples for 160 subjects. This paper used the palmar samples, of which there are 640.

![FYODB Sample Image](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%202.png)

FYODB Sample Image

### **DorsalVein Dataset**

- Initially we wanted to use the PUT PalmVein Dataset, but due to lack of public availability the DorsalVein Dataset was used as a substitute.
- DorsalVein Dataset consists of 1,104 images from 138 different subjects.

![DorsalVein Sample Image](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%203.png)

DorsalVein Sample Image

# Data Preparation

### 1. Region Of Interest (ROI) Extraction

- The images were initially prepared by extracting their regions of interest (ROI).
- Involves cropping out background and extra areas like fingers and wrist, to ensure focus on the veins only.
- In this study the ROI images were already available in the dataset files.

![Original FYODB Image vs ROI Image](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%204.png)

Original FYODB Image vs ROI Image

### 2. Data Augmentation

- Since the CNN models are trained from scratch without transfer learning, there is a need of high data volumes to ensure generalization.
- For this purpose, each dataset was augmented using Keras Image Generator to increase the number of samples per class.
- This greatly increased the number of samples for each dataset, for e.g, FYODB size was increased from 640 images to 6,400 and DorsalVein size was increased from 1,104 to 5,520
- Augmentations applied include rotation, width shift, height shift, shearing, zooming, flipping, and brightness changing.

![VERA Sample Augmented Image](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%205.png)

VERA Sample Augmented Image

![FYODB Sample Augmented Image](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%206.png)

FYODB Sample Augmented Image

![DorsalVein Sample Image](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%207.png)

DorsalVein Sample Image

# CNN Models

### AlexNet

- AlexNet is a simple yet extremely successful CNN architecture, originally trained on the ImageNet dataset.
- It consists of 5 blocks with only one convolutional layer in each (11x11 filter to 3x3 filter), followed by ReLU activation, Batch Normalization, and Max Pooling with a 3x3 filter (see architecture below).
- A major contribution of this paper was to reduce the number of filters and filter size per CONV layer for each CNN model, thus greatly reducing training time while upholding model efficiency and accuracy.
- The reduction in filters made in the AlexNet architecture is shown below.

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%208.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%209.png)

### VGG16

- VGGNet is a family of CNN models with slightly different architectures.
- The 16 in VGG16 means that it has 16 CONV layers, spread out in 5 blocks.
- All CONV layers use ReLU activation function and 3x3 filter size, followed by Batch Normalization and Max Pooling with a 3x3 filter and stride of 2.
- The reduction in filters made in the VGG16 architecture is shown below.

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2010.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2011.png)

### VGG19

- VGG19 is another member of the VGGNet family of CNN models.
- It consists of 19 CONV layers spread out in 5 blocks.
- The architecture of VGG19 is identical to VGG16, but with the addition of an additional CONV layer in blocks 3, 4 and 5.
- The reduction in filters made in the VGG19 architecture is shown below.

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2012.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2013.png)

# Hyperparameters

| Hyperparameter | Value |
| --- | --- |
| Training Epochs | 30 |
| Loss Function | Sparse Categorical Cross-Entropy |
| Optimizer | Adam |
| Learning Rate | 10^-4 |
| Callback Functions (FYODB and DorsalVein only) | Reduce LR on Plateau |

# Results

### VERA PalmVein Dataset

| CNN Model | Test Accuracy | Computation Time |
| --- | --- | --- |
| AlexNet | 98.86% | 92.03s |
| VGG16 | 94.89% | 775.11s |
| VGG19 | 97.44% | 419.39s |

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2014.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2015.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2016.png)

### FYODB Dataset

| CNN Model | Test Accuracy | Computation Time |
| --- | --- | --- |
| AlexNet | 95.90% | 144.15s |
| VGG16 | 95.70% | 962.15s |
| VGG19 | 95.51% | 1047.67s |

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2017.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2018.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2019.png)

### DorsalVein Dataset

| CNN Model | Test Accuracy | Computation Time |
| --- | --- | --- |
| AlexNet | 97.56% | 134.37s |
| VGG16 | 99.84% | 808.03s |
| VGG19 | 97.91% | 865.49s |

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2020.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2021.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2022.png)

# Decision-Level Fusion (Ensemble)

- Decision-Level Fusion was used after all models were trained to combine their inference power.
- Creating an ensemble of models allows for more accurate predictions; each model overcomes the shortcomings of the other.
- The fusion technique used involves gathering predictions from each model, assigning a weight of 1 to correct and 0 to incorrect prediction, and adding the weights.
- A sum ≥ 2 indicates a correct prediction by the ensemble.
- However we also tried a slightly modified fusion method that yielded better results with higher accuracy.
- It involved creating a set of predictions from each model, and simply taking the mode of that set to yield the ensemble prediction. This decision is then compared with the label to judge correctness.
- The improved fusion technique yields slightly higher accuracy

### Decision Level Fusion - Results

| Dataset | Fusion Accuracy | Modified Fusion Accuracy |
| --- | --- | --- |
| VERA PalmVein | 98.86% | 99.15% |
| FYODB | 96.97% | 97.46% |
| DorsalVein | 98.95% | 99.19% |

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2023.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2024.png)

![Untitled](Palm%20Vein%20Recognition%20using%20CNNs%205061ea292264492088b10d63ac77f9ae/Untitled%2025.png)

# Conclusion

- This study successfully implemented a robust and accurate system for Palm-Vein biometrics that produces very strong results on three different datasets.
- If implemented, this framework can allow for very high security in crucial infrastructure such as the banking or government sector.
- The results also demonstrate the power of ensemble models and the importance of the technique used to perform the decision fusion of the individual models.