# whatever this is &darr; 

Making 0 assumptions about what the Probability Density Function is - no parameters. <br>
Divide the data into histograms. 
- The choice of the **bin width** can impact the conclusions!!!

Patterns of a class should be grouped/clustered together in feature space. Objects that are near one another should have similar features.

Probability (x lies in a small range of length V) = k/N <br>
Probability (x lies in ... ) = ... 

<center>
pV = k/N &rarr;  p = k/NV
</center>

### Kernel Density Estimation
Computing a weighting, so data points very close to *x* contribute a lot, and points further from *x* contribute little.

<center>

</center>

V is critical :
- too small &rarr; spiky pdf [low bias, high variance]
- too big &rarr;  over-smoothed [high bias, low variance]


- Easier to classify data if we know the underlying distributions.
- Parametrically,
- Non-




# Clustering
- Detects patterns.
	- e.g. in customer shopping behaviours : results, regions of images, etc...
- Useful when we don't know what we're looking for a priori.


We look at the data for which groups are unknown and undefined, and try to learn the groups themselves, as well as what differentiates them.

Clustering Algortihms
--------------------------------------------------
1. Parition Algorithms
	- no hierarchy.
1. Hierarchical Algorithms
	- Bottom Up - **Agglomerative**.
	- Top Down - **Divisive**

#### K-Means Algorithm
Simple partitioning approach based on the idea of centroids (center) or prototypes.

1. Select K points as initial centroids.
1. While centroids changing : 
	1. Form K clusters by assigning each point to its nearest centroid.
	1. Recompute centroid of the cluster.

#### Disadvantages of K-Means
- Need to know K in advance.
	- could try out several K's and select the best?
- May converge on local minimum.
	- i.e. suboptimal clustering.
- Each point is only assigned to a single cluster (hard clustering).
- Flat strucutre (no clusters within clusters).
		

#### Advantages of K-Means
- Fast.
	- just groing through and looking how near everything is to a K.

