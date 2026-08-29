# Image Recognition & Classification with Keras in R

**Name:** Sneha Gadhari
**Roll No.:** 23102B0055
**Experiment:** R Programming Lab 4 — Project Implementation & Version Control using GitHub

## Objective
Implement an image classification pipeline in R using Keras and EBImage, training a neural network to classify images into two categories, and manage the project using Git/GitHub.

## Dataset
- 12 images total, 2 classes ('p' and 'c'), 6 images per class
- Images uploaded directly into the Colab session (see `dataset/` folder)

## R Packages / Libraries Used
- `EBImage` (Bioconductor) — image reading and preprocessing
- `keras` — building and training the neural network (TensorFlow backend)

## Major Operations Performed
1. Install and load EBImage + Keras (with TensorFlow backend via `install_keras()`)
2. Read images using `readImage()`
3. Resize/normalize images to consistent dimensions
4. Reshape image data into matrix format for input to dense layers
5. Split into training/test sets
6. One-hot encode labels using `to_categorical()`
7. Build a sequential dense neural network (256 → 128 → 2 units)
8. Compile model with `categorical_crossentropy` loss, RMSprop optimizer
9. Train for 30 epochs, batch size 32, 20% validation split
10. Evaluate on test set, generate confusion matrix

## Instructions to Execute
1. Open `RProg_Experiment_4_23102B0055.ipynb` in Google Colab
2. Set runtime to R
3. Upload `dataset/` folder (images) into the Colab session
4. Run all cells top to bottom

## Results
- Test accuracy: **90%**
- Confusion matrix:

|           | Actual 0 | Actual 1 |
|-----------|----------|----------|
| Predicted 0 | 5      | 1        |
| Predicted 1 | 0      | 4        |

## Repository Structure
```
Experiment-4/
├── dataset/
├── RProg_Experiment_4_23102B0055.ipynb
├── R_Prog_Experiment-4_23102B0055_Sneha_Gadhari.docx
└── README.md
```
