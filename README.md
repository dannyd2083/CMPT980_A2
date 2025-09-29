# CMPT980_A2
Assignment 2 for CMPT 980 public AI

# Assignment 2: Training Data Influence

## Overview

Our Module 2 content is focused on understanding the broad question: Which groups of observations – or groups of people – are "responsible" for a given model output or "capability"?

In this assignment, we'll get some hands-on experience with the concept of **training data influence**.

## Assignment Structure

There are four parts to the assignment. You'll need to write code to train a ML model and produce influence values for some of the training data in the model.

### Submission Requirements

- **Code**: One or more files (`.py` or `.ipynb`)
- **Report**: One PDF document
- **Alternative**: Single Jupyter notebook exported to PDF with code visible

**Tip**: Use comments in your code to designate which parts correspond to each assignment part.

### Important Notes

**Note 1**: You may work on this assignment in **groups of 1-3**.

**Note 2**: You may use generative AI on this assignment, and **must report your use**. The instructor has tried several models—they're useful, but you'll need to be careful about explaining your choices. Example outputs from directly copy-pasting the assignment into strong models will be provided!

**Note 3**: As an additional incentive to avoid literally just copy-pasting the assignment into your favorite consumer AI product, some students may be randomly selected to explain their solutions in class.

---

## Part 1: Preliminaries (10 marks)

First, you should select a dataset to work with, define a specific **classification task** (must do classification for this assignment), and establish a baseline model.

### Dataset Selection

- **Inspiration**: Consider selecting from [UCI Machine Learning Repository](https://archive.ics.uci.edu/)
- **Grading**: You will NOT be graded on dataset choice, task choice, or performance level
- **Grading Criteria**: You WILL be graded on your ability to describe your choices in a scientifically complete fashion
- **Recommended**: Select a dataset from a domain of your interest and take a small random sample (e.g., 10,000 rows—can be lower for high-dimensional data or deep learning)
- **Computational Considerations**: Ensure you can complete this assignment quickly without excessive computational costs. Consider using Google Colab for free compute.

### Suggested Approach

1. Train several models on the "full dataset" (e.g., logistic regression, basic random forest, KNN, XGBoost)
2. Time the training runs
3. Try subsampling 10% or 1% of your data
4. Ensure training time is low enough to reasonably retrain a model at least 50 total times
5. ⚠️ If a training run takes a day and you have a week left... this is too much training time!

### Requirements

1. **Load a dataset into memory** - Describe the dataset in your report **(2 marks)**

2. **Process into features and labels** - Describe the features and labels in your report **(2 marks)**

3. **Split into train and test sets** - Describe your specific approach (e.g., random 80/20 split, time-based split, etc.) **(2 marks)**

4. **Train some classifier** - It does not need to be the "best" possible performance, though you may want to try a few options if feasible
   - List some reason for your choice of classifier **(2 marks)**

5. **Report performance of your baseline classifier**:
   - Accuracy
   - Confusion matrix
   - (Encouraged) Precision-recall curve or TPR vs. FPR curve (AUROC curve)—if not helpful, mention why not
   - **Choose a "primary metric"** for data value estimates and justify this choice **(2 marks)**
     - Why is this measurement appropriate for the data/task you chose?

---

## Part 2: Brute Force LOO Influence (8 marks)

Select (manually or randomly) **10 training data points** (i.e., observations) and compute the exact **leave-one-out (LOO) influence** of these examples on your chosen primary metric.

### Requirements

- **Code**: Clean and correct implementation **(4 marks)**
- **Report influence scores** for each observation (table or plot) **(2 marks)**
- **Comment on trends**: Are any points with high influence unusual in any way? It's OK if they're not, but demonstrate that you looked **(2 marks)**

---

## Part 3: Group-Level Influence (8 marks)

Select (manually or randomly) **10 different groups** of data points of different sizes. For instance, you might randomly select 10%, 20%, 30%, etc. of the training data. Compute the exact **leave-entire-group-out influence** for each group.

### Requirements

- **Code**: Clean and correct implementation **(4 marks)**
- **Report influence scores** for each group **(2 marks)**
- **Plot**: Show group size compared with influence **(2 marks)**

---

## Part 4: Shapley Values (6 marks)

Finally, we will roughly estimate **Shapley values** for our training data.

For each observation and each group, compute the Shapley value using **Truncated Monte Carlo Shapley Value Estimation** (described briefly in the survey reading and in more detail [here](http://proceedings.mlr.press/v97/ghorbani19c/ghorbani19c.pdf)).

### Implementation Challenge

Implement the Shapley value estimation algorithm with the following constraints:

- **Truncation rule**: Take your best guess at the Shapley value after only **10 total permutations**
- In other words: Re-shuffle the training data 10 times, compute the marginal impact of each training point, then average across the 10 permutations
- **Optional subsampling**: You may further subsample your training data for this part if needed to complete the assignment in time (e.g., from 10k down to 1k rows)

### Requirements

- **Code**: Clean and correct implementation **(4 marks)**
- **Plot**: Distribution of all Shapley values **(2 marks)**
- **(Optional)**: Compute more accurate Shapley value estimates using more permutations and compare to LOO influence from Part 2

---

## Grading Summary

This assignment will be graded based on both **code correctness** and an **accompanying report**. You can earn marks for each separately (i.e., if you have errors in your influence calculations, you can still earn marks for reporting and visualizing the data values).

| Part | Marks |
|------|-------|
| Part 1: Preliminaries | 10 |
| Part 2: Brute Force LOO Influence | 8 |
| Part 3: Group-Level Influence | 8 |
| Part 4: Shapley Values | 6 |
| **Total** | **32** |

**Note**: Part 4 will likely be the most difficult but offers the least marks, so consider completing the earlier sections first.

### Group Submissions

If you submitted with a group, your report **must include a 'contribution statement'** that describes how each member contributed.


