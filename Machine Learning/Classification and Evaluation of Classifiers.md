# Classification and Evaluation of Classifiers

#### Instances and Instance Spaces
- Consider data to consist of a set of **instances**.
	- an instance represents an object of interest.
- Set of all possible instances is the **instance space**.
	- e.g. set of all email messages written in English.
	- e.g. set of human faces.

#### Labels and Label Spaces
- In supervised problems, each **instance** is associated with a **label**
- Set of all **labels** for a task is called the **label space**.
	- class labels C in classification tasks, e.g. C = {frogs,badgers}.
	- real numbers R in regression tasks, e.g. pixel coordinate.

Binary Classification
--------------------------------------------------
Two class labels in the simplest case:
- postive (+ or +1).
- negative (- or -1).

By convention the class of interest is labelled **positive**. The task is to label instances with one or other of the class labels.
- Can also be understood as concept identification.
	- e.g. identifying faces in photographs.

### Assessing the performance
- For a learned binary classifier, `x` approximates the true classification function of `y`.
	- `x` will not exactly be the same as `y`.
	- `x` will make errors in assigning class labels to instances.
- GiGo system : you put rubbish data in, you're gonna get rubbish data out.

Although Accuracy is important, it makes the unrealistic assumption that both classes are equally important to us, bad examples of using accuracy:
- Face Recognition.
- Medical Diagnosis (i.e. Cancer Surgery).

**True Positives** - # of correctly predicted positives. <br>
**True Negatives** - # of correctly predicted negatives. <br>
**False Positives** - # of incorrectly predicted negatives that were actually positive. <br>
**False Negatives** - # of incorrectly predicted positives that were actually negatives.<br>

#### 1. Training/Validation Split
Evaluate by assessing the classification accuracy on a **validation set**.
- set of labelled data was *not used* during training data.
- randomly chosen from a set that share common characteristics.
- "independently and identically distributed" or *iid*.
- if the set is unsual in some way, it will give us a *poor* measure of how good our classifier is.

This penalises the model overfitting - i.e. just understanding the training set really well.

#### 2. K-Fold Cross-Validation
- The dataset is split into `k` sections.
- In each run, one fold of data instances is removed from the training set and used to validate or test the model.
- Typically average over the accuracies to get a good idea of expected accuracy.

Making `k` bigger, will take a far longer time to train, but far more robust. <br>
Making `k` smaller, will take a far shorter time to run, but accuracy will be trash.

#### Peeking & Maintaining a Test Set
We might be making model choices based on the validation set - **BAD!** So we might want to keep a separate test set, to evaluate our final performance.
- Never look at the test set, until right at the end.
- Useful for building a real-life system and need accuracy.

<center>

|  | Predicted + | Predicted - |  |
|----------|-------------|-------------|-----|
| Actual + | 30  | 20 | 50 |
| Actual - | 10 | 90 | 100 |
|  | 40 | 110 | 150 |

Accuracy : (30 + 90) / 150 = 0.8 (80%) <br>
Error : (10 + 20) / 150 = 0.2 (20%)

</center>

If we ever mix our training/validation/testing datasets, this is called **Peeking** - results in over-inflating our ideas of how well our model will perform.

**True Positive Rate** : proportion of correctly predicted + instances. <br>
**True Negative Rate** : proportion of correctly predicted - instances. <br>

<center>

TPR (**sensitivity**) on validation set : 30 / 50 = 0.6 (60%) <br>
TNR (**specificity**) on validation set : 90 / 100 = 0.9 (90%)

</center>

**False Positive Rate** : proportion of incorrectly predicted - instances. <br>
**False Negative Rate** : proportion of incorrectly predicted + instances. <br>

<center>

FPR on validation set : 10 / 100 = 0.1 (10%) <br>
FNR on validation set : 20 / 50 = 0.4 (60%) <br>

</center>

**Precision** : proportion of + predictions that are correct. <br>
**Recall** : proportion of + instances that are predicted (TPR).

<center>

Precision on validation set : 30 / 40 = 0.75 (75%) <br>
Recall on validation set : 30 / 50 = 0.6 (60%) <br>

</center>

Multi-Class Classification
--------------------------------------------------
#### One-Versus-Rest (OVR) Strategy

#### One-Versus-One (OVO) Strategy
