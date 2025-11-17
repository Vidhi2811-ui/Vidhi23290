# Community Detection in Zachary's Karate Club using Spectral Modularity
-Vidhi Kishor Sayam
-IMS23290
1.Overview of the project
The project signifies the community detection algorithm of the famous Zachary's Karate Club using Spectral Modularity Maximization.The motive behind this assignment is to use an iterative spectral modularity detection method to compare the detected partiotion to the real split observed by Zachary.
A key part of the analysis is to implement the s[ectral modularity an study how network metrices such as degree,betweeness,closeness and clustering evolve during recrusive community splits.It also helps us to understand how modularity measures the quality of a graph partition,how recrusive bisection can reveal more than two communities,and the structural roles of nodes reflected in centrality metrices.
This project is a overall excercise in network analysis,eigenvectors,clustering evlove during community splits and data visualization.

2.Key Features and the tasks involved :
Task 1 — Build the Modularity Matrix
Compute adjacency matrix A, degree vector 𝑘, and total edges 𝑚.
Construct the modularity matrix 𝐵.

Task 2 — Perform Spectral Bipartition
Compute the leading eigenvalue and leading eigenvector of 𝐵
Assign nodes to two communities based on sign of the eigenvector entries.

Task 3 — Recursive Community Splitting
For each discovered community subset:

1.Form the restricted modularity matrix 𝐵(𝐶).
2.Compute its leading eigenvalue.
3.If eigenvalue > 0, split further; otherwise stop.
Continue until all communities are indivisible.

Task 4 — Graph Visualization
After each split, plot the network using a constant layout.
Use different colors for different communities.
Label all nodes.

Task 5 — Compute Node Metrics After Each Iteration
For every stage of recursion:
1.Degree centrality
2.Betweenness centrality
3.Closeness centrality
4.Clustering coefficient
Store the metrics for each node and each iteration.

Task 6 — Plot Metric Evolution
Create line or bar plots showing how each node’s metrics change across recursion levels.
Use legends and consistent node labels.
