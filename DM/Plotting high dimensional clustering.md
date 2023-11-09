[LOOK HERE](https://stats.stackexchange.com/questions/52625/visually-plotting-multi-dimensional-cluster-data)

Basically the methods are
*parallel coordinates plot (PCP)*
To visualize how each attributes contributes.
Normalizing axis is recommended.
Be aware of the order of axis to discover interesting correlations.
Downside: over-cluttered. Apply "brushing" to highlight a selected line or collection of lines, fading out the others.
![[Pasted image 20231109114435.png|400]]
[source](https://towardsdatascience.com/parallel-coordinates-plots-6fcfa066dcb3)



*scatterplot on principal components*
Basically a biplot with colored clusters to add the 3rd dimension, which is the cluster label.
A PCA is required to choose the two axis to represent. They are the most interesting attributes.

*scatterplot of distance from centroids*
Each cluster will fall on one side on the diagonal line.
![[Pasted image 20231109113949.png|400]]

*scatterplot matrix colored by cluster*
To see pairwise relations compared to the clustering.
![[Pasted image 20231109114132.png|400]]