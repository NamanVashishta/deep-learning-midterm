# Deep Learning Midterm: Math Answer Verification

[cite_start]**Naman Limani (nl2833@nyu.edu) & Naman Vashishta (nv2375@nyu.edu)** [cite: 2, 3]
[cite_start]*CS-GY 6953 / ECE-GY 7123 Deep Learning - Fall 2025* [cite: 3]

---

## 1. Project Overview

This repository contains the code for our submission to the Math Question Answer Verification Competition. [cite_start]The goal was to build a binary classifier to determine if a given mathematical solution is correct, using a fine-tuned **Llama-3 8B** model[cite: 5].

[cite_start]Our final model achieves a **test accuracy of 0.833** [cite: 7, 81][cite_start], a significant improvement over the competition baseline of 0.726[cite: 69].

## 2. Key Finding: The Importance of the Prompt

Our primary finding was that the model's performance is critically dependent on prompt engineering.
* [cite_start]**Failed Approach:** An initial prompt containing only the "Question" and "Solution" failed, yielding **0.46 accuracy**[cite: 62, 69]. The model was trying to *solve* the problem rather than *verify* it.
* [cite_start]**Successful Approach:** By adding the **"Expected Answer"** as explicit context to the prompt, we enabled the model to correctly perform the verification task, raising the accuracy to **0.833**[cite: 63, 78].

[cite_start]We also found that a shorter **max sequence length of 1024** was optimal [cite: 22, 87][cite_start], outperforming models trained on longer 2048 or 4096-token contexts[cite: 93].

## 3. Repository Contents

* `final_training_script.ipynb`: (Please rename your 1024-seq-length training script to this) The script used to train our final model (50k samples, 1024 seq length).
* `model_3_testing.ipynb`: The reproducible inference script to generate predictions on the test set.
* `Deep_learning.pdf`: Our final project report detailing all experiments and analysis.

## 4. How to Reproduce (Inference)

1.  **Download Model Weights:** Our final LoRA adapter weights are available on Google Drive:
    * **Link:** [https://drive.google.com/drive/folders/1SVnnSkvj6BwEmJnmZ1cE6g0mfvCxj8Cv](https://drive.google.com/drive/folders/1SVnnSkvj6BwEmJnmZ1cE6g0mfvCxj8Cv)

2.  **Run Inference Notebook:**
    * Open `model_3_testing.ipynb`.
    * Update the `CHECKPOINT_PATH` variable in **Cell 5** to point to the location where you downloaded the model weights.
    * Run all cells in the notebook. This will generate the `submission.csv` file, which produces 3,611 True and 6,389 False predictions, matching our final 0.833 accuracy submission.
    
