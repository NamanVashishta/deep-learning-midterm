# Deep Learning Midterm: Math Answer Verification

**Naman Limani (nl2833@nyu.edu) & Naman Vashishta (nv2375@nyu.edu)**
*CS-GY 6953 / ECE-GY 7123 Deep Learning - Fall 2025*

---

## 1. Project Overview

This repository contains the code for our submission to the Math Question Answer Verification Competition. The goal was to build a binary classifier to determine if a given mathematical solution is correct, using a fine-tuned **Llama-3 8B** model.

Our final model achieves a **test accuracy of 0.833**, a significant improvement over the competition baseline of 0.726.

## 2. Key Finding: The Importance of the Prompt

Our primary finding was that the model's performance is critically dependent on prompt engineering.
* **Failed Approach:** An initial prompt containing only the "Question" and "Solution" failed, yielding **0.46 accuracy**. The model was trying to *solve* the problem rather than *verify* it.
* **Successful Approach:** By adding the **"Expected Answer"** as explicit context to the prompt, we enabled the model to correctly perform the verification task, raising the accuracy to **0.833**.

We also found that a shorter **max sequence length of 1024** was optimal, outperforming models on longer 2048 or 4096-token contexts.

## 3. Repository Contents

This repository includes all scripts for training and inference for our experiments.

* **Final Model (0.833 Accuracy):**
    * `model_3_training.ipynb`: The notebook used to train our final model (50k samples, 1024 seq length).
    * `model_3_testing.ipynb`: The reproducible inference script for our final model.

* **Experimental Models:**
    * `model_1_training.ipynb` / `model_1_inference.ipynb`: 60k samples, 4096 seq length (Exp 1).
    * `model_2_training.ipynb` / `model_2_inference.ipynb`: 30k samples, 2048 seq length (Exp 2).

* **Report:**
    * `Deep_learning.pdf`: Our final project report detailing all experiments and analysis.

## 4. How to Reproduce (Final Model)

1.  **Download Model Weights:** Our final LoRA adapter weights are available on Google Drive:
    * **Link:** [https://drive.google.com/drive/folders/1SVnnSkvj6BwEmJnmZ1cE6g0mfvCxj8Cv](https://drive.google.com/drive/folders/1SVnnSkvj6BwEmJnmZ1cE6g0mfvCxj8Cv)

2.  **Run Inference Notebook:**
    * Open `model_3_testing.ipynb`.
    * Update the `CHECKPOINT_PATH` variable in **Cell 5** to point to the location where you downloaded the model weights.
    * Run all cells in the notebook. This will generate the `submission.csv` file, which produces 3,611 True and 6,389 False predictions, matching our final 0.833 accuracy submission.
