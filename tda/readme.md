# Bank Marketing Data Set

The data is related with direct marketing campaigns (phone calls) of a Portuguese banking institution. The classification goal is to predict if the client will subscribe a term deposit (variable y).

## Constructing distance matrix

We first onehot-encode the categorical variables. We remove the "call duration" variable, as it is not available at test time. Then we use K-means (via Scikit-learn) to create 50 clusters. For every sample in a cluster we create a 50-dimensional vector with the distances to all other clusters. We compute the 50-dimensional mean of each cluster member cluster distances. For every 50-dimensional cluster mean we compute Euclidean distance to every other 50-dimensional cluster mean. This is our distance matrix.

## Constructing tree

We use version 1.0.8 of the maketree utility (via CompLearn). This algorithm uses Markov-Chain Monte-Carlo to optimize the Minimum Quartet Tree Cost. We obtain a tree with a fitness of ~0.998, exported as a .dot file.

We write a small parser for Python to run through the .dotfile and output a tree with D3.js and HTML5.

## Data-driven

To use the tree to aid a data-driven approach/exploration, we color the nodes by their signal ratio. This allows us to identify clusters/nodes with a high, or low, signal ratio. It also visually tells us if the constructed tree is informative.

We also look at the mean of a variables in a cluster vs. the mean of a variable in the entire dataset. If this is 1, 2, 3 standard deviation above or below the dataset mean, we show this inside a tooltip.

From the tree we can get a few quick insights:

- Older customers subscribe a term deposit more often
- Retired customers subscribe more often
- When poutcome=success is above average customers subscribe more often
- When Month=aug, sep, oct, mar, apr, dec is above average customers subscribe more often
- Low Euribor3m customers subscribe more often
- Low pdays customers subscribe more often
- High "campaign" customers subscribe less often
- Low "contact=cellular" customers subscribe less often
- Younger customers subscribe to a term deposit less often

See: http://mlwave.github.io/tda/bake.html for live version.

## References

[Bostock et al., 2007] M. Bostock. D3.JS https://d3js.org/

[Cilibrasi et al., 2008]  R. Cilibrasi, A. Lissa Cruz, S. de Rooij. CompLearn. http://complearn.org/

[Pedregosa et al., 2011] Pedregosa, F. and Varoquaux, G. and Gramfort, A. and Michel, V. and Thirion, B. and Grisel, O. and Blondel, M. and Prettenhofer, P. and Weiss, R. and Dubourg, V. and Vanderplas, J. and Passos, A. and Cournapeau, D. and Brucher, M. and Perrot, M. and Duchesnay, E. Scikit-learn: Machine Learning in Python. http://scikit-learn.org/stable/

[Arthur et al., 2007] D. Arthur, S. Vassilvitskii. k-means++: The advantages of careful seeding. Proceedings of the eighteenth annual ACM-SIAM symposium on Discrete algorithms, Society for Industrial and Applied Mathematics (2007) http://ilpubs.stanford.edu/778/1/2006-13.pdf

[Singh et al., 2007] G. Singh, F. Mémoli, G. Carlsson. Topological Methods for the Analysis of High Dimensional Data Sets and 3D Object Recognition. Eurographics Symposium on Point Based Graphics, European Association for Computer Graphics, 2007 https://research.math.osu.edu/tgda/mapperPBG.pdf

[Carlsson, 2009] G. Carlsson. Topology and data. Bull. Amer. Math. Soc. 46. http://www.ams.org/images/carlsson-notes.pdf

[Ramachandran, 2016] M. Ramachandran. A Horizontal Solution to a Vertical Problem: Why Segmentation Matters to Banks. Ayasdi Blog. http://www.ayasdi.com/blog/financial-services/5669-2/

[Cilibrasi et al., 2014] R. Cilibrasi, P. Vitanyi. A Fast Quartet Tree Heuristic for Hierarchical Clustering. Arxiv. http://arxiv.org/abs/1409.4276

[Moro et al., 2014] S. Moro, P. Cortez and P. Rita. A Data-Driven Approach to Predict the Success of Bank Telemarketing. Decision Support Systems, Elsevier, 62:22-31, June 2014 http://www.sciencedirect.com/science/article/pii/S016792361400061X
