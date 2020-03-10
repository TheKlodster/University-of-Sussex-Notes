# Lecture 1 : Introduction

### Coursework :
**100% of the module**
- 40% code & data analysis.
- 60% 2-page report.


--------------------------------------------------
### Three main ingredients of Machine Learning :
- **Tasks**
	- problems that require a mapping from data to desired inputs (insights).
- **Features**
	- characteristics of the data used to describe domain objects.
- **Models**
	- encode the required task mapping.		

--------------------------------------------------
#### Machine Learning Tasks if you have Health Data
- **Classification**
	- binary classification involves separating data into two distinct groups.
		- e.g. distinguishing people at risk from heart disease (+) from those not as risk (-).
- **Regression**
	- involves mapping from data items to real values.
		- e.g. *quantifying* the risk of heart disease on the basis of personal health records.
- **Clustering**
	- separating data into different *clusters/concepts* on the basis of their characteristics.
		- e.g. *grouping people* according to their genetic characteristics.
- **Collaborative filtering**
	- identifying rules or associations from data.
		- e.g. *"recommending" diseases* on the basis of patient records and diseases of similar patients.
- **Dimensionality reduction**
	- visualising the data.

Teaching Your Models
--------------------------------------------------
#### Supervised Learning
Each element of the training data has associated *labels* :
- labels are the output for this data example.
	- e.g. binary classification : patiebt data already labelled with "*at risk of heart disease*" or "*not at risk of heart disease*".
- model should **generalise** from training data.
	-i.e. be good at predicting output for unseen data.

#### Unsupervised Learning
These mthods do not require labels :
- learns structure & patterns based on the similarities and differences in the data deatures for the training examples.
	- e.g. clustering : grouping people on basis of genetic similarity in order to discover interesting sub-groups.

#### Degrees of Supervision
**Semi-Supervised** machine learning methods use labels on a *subset* of the data. This is relevant when the labels are **expensive**.
