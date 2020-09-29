*Lectures 3 & 4, 4th & 5th Febraury*
# Pre-Processing
Pre-processing need not be optimal, but applying some human intelligence in this step can enhance and speed up the performance of the artificial intelligence in network training.

Input Data -> Pre-Processing -> Network/Model Optimisation -> Post-Processing -> Output

Post-processing only involves passively re-mapping the network output into its raw form.

**Input Normalisation** : normalise data to be in the same scale and have zero mean.
- useful for network training and visual inspection.
- aids visualisation.
- generally improves performance of model training.


**Dimensionality Reduction** : reduce the number of dimensions.
- define a few new variables that are combinations of raw variables, and account for most of the variance.
- some information will be lost.

Why do this?
- computationally expensive to store & work with high dimensional spaces.
- fewer parameters to learn.
- discover intrinsic dimensionality of the data.

E.g. image processing - 1 dimension for every pixel in the image.

**Feature Selection** : include & exclude attributes in the data without changingthem.
- automatically or manually.
- will lead to information lost.


**Feature Extraction** : use combination of input variables.
- this approach can incorporate any of the first 3.
- reduces overfitting : less redundant data means less opportunity to make decisions based on noise.
- improves accuracy : less misleading data means modeling accuracy improves.
- reduces training time : fewer data points reduces algorithm complexity and algorithms train faster.

--------------------------------------------------
#### Random Subset Selection
- Sequential Forward Search
	- sequentially select features until there is no improvement in prediction.
	- select 1 feature, train and test model.
	- add another feature, train and test model.
	- iterate until there is no further improvement in prediction.

#### Principal Components Analysis (PCA)
- Transform the data into a lower dimensional space losing as little information as possible.

We measure availability by computing the variance of the variables.

The idea is to:
- **(i) change the coordinates** (rotate the axes), so that the off-diagonal covariance terms are 0.
- **(ii) rank the variances** of the newly defined features in the new coordinate system.
- **(iii)** selected features are those corresponding to the largest *d* variances, where *d* is how many features are kept.

##### Does PCA work well?
No! 
- When the relationship between components is very non-linear, it doesn't work well.
- When components with small variability really matter, PCA will make mistakes due to the *unsupervised* nature of the process.

##### Where does PCA work best?
- For Gaussian distributed data, i.e. when the inputs have a normal distribution.

#### Pre-processing before doing PCA
Input normalization:
- Must subtract the mean as the theory requires that the data 
are centred at the origin
- Also, we divide by the standard deviation as results shouldn’t 
depend on the units of the inputs.


Don’t do whitening! PCA does the whitening. If you do it 
before PCA it will destroy the correlations that are key to doing 
PCA!

E.g. Face Recognition
- The dimensionality of a face image is extremely high.
