## NANO706 · Assignment 2 · Rutuja S. Bhamare

*Three questions. Two notebooks. One lesson in evaluating predictions*

`CLASSIFY WINE → RECOGNIZE DIGITS → DETECT OBJECTS`

</div>

> What makes a prediction convincing: a perfect score, a stronger model, or a box drawn in the right place? These homework experiments examine each kind of evidence.

Scope of this report

This report covers only the work under **HomeWork** in Part 1 and **HomeWork2** in Part 2. Results and figures come from the saved notebook outputs. The earlier housing, Iris, clustering, CNN, and sample-image demonstrations are excluded.

Investigation | Input | Task | Recorded evidence |
| :-- | :-- | :-- | :-- |
| 01 · Chemical fingerprints | Wine measurements | Compare SVM, Decision Tree, and Logistic Regression | Test accuracies and a confusion matrix |
| 02 · Reading handwriting | MNIST pixel values | Compare Random Forest, Logistic Regression, and MLP | Test accuracies on a shared split |
| 03 · Beyond the benchmark | A personal photograph | Run pretrained YOLO inference | Annotated image and qualitative inspection


## Part 1: Wine Classification

The Wine dataset contains 13 chemical features and three wine classes. Although the notebook refers to wine quality, the target represents wine classes rather than quality ratings.

I plotted alcohol against malic acid and split the data into 70% training and 30% testing using `random_state=101`. All 13 features were used for classification.

<img width="778" height="547" alt="image" src="https://github.com/user-attachments/assets/1b8d51b2-76d4-4b13-8a9a-bbe8819d6f78" />

| Model | Test accuracy |
|---|---:|
| SVM (linear kernel) | 0.96 |
| Decision Tree | 0.93 |
| Logistic Regression with standardization | 1.00 |

Logistic Regression correctly classified all 54 test samples. Its confusion matrix was:

[[19  0  0] <br>
 [ 0 22  0] <br>
 [ 0  0 13]]
 
This was the best result on this split, but a perfect score on a small test set does not guarantee perfect performance on new data. Cross-validation would help check its consistency.

## Part 2: MNIST Classification

MNIST images were represented by 784 pixel values, normalized to `[0, 1]`. An 80/20 split with `random_state=42` gave 56,000 training images and 14,000 test images.

| Model | Configuration | Test accuracy |
|---|---|---:|
| Logistic Regression | `max_iter=2000` | 92.02% |
| Random Forest | 100 trees | 96.75% |
| MLP | 128 hidden units, early stopping | 97.07% |

The MLP achieved the highest accuracy, though it was only 0.32 percentage points ahead of Random Forest. All three models used the same normalized inputs and test split.

## Part 3: YOLO on a Personal Photograph

I loaded pretrained YOLOv5s weights and ran inference on my photograph.

<img width="1600" height="1200" alt="face-detection" src="https://github.com/user-attachments/assets/d575abc3-be32-4ad0-a426-e14ef8342be4" />

The model detected a person with a confidence score of 0.96. It also labeled parts of the poster and badge area as a book and cell phone, which appear incorrect.

The assignment asks for face detection, but this output shows a person box rather than a separate face box. I went a step further and used a pretrained YOLOv8 face detection model on the same photograph to detect the face specifically.

<img width="4032" height="3024" alt="self_image" src="https://github.com/user-attachments/assets/b71d2408-a570-452a-b3b9-a5157e5c7903" />


## Conclusion

Logistic Regression performed best on the Wine test split, while MLP had the highest MNIST accuracy. The YOLO example showed why visual inspection matters: detecting a person successfully does not necessarily mean detecting their face.

*Results and images are taken from the saved outputs in the HomeWork and HomeWork2 sections of the submitted notebooks.*
