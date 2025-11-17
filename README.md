# Community Detection in Zachary's Karate Club using Spectral Modularity
-Vidhi Kishor Sayam
-IMS23290

# 1.Overview of the Project

The project signifies the community detection algorithm of the famous Zachary's Karate Club using Spectral Modularity Maximization.The motive behind this assignment is to use an iterative spectral modularity detection method to compare the detected partiotion to the real split observed by Zachary.
A key part of the analysis is to implement the s[ectral modularity an study how network metrices such as degree,betweeness,closeness and clustering evolve during recrusive community splits.It also helps us to understand how modularity measures the quality of a graph partition,how recrusive bisection can reveal more than two communities,and the structural roles of nodes reflected in centrality metrices.
This project is a overall excercise in network analysis,eigenvectors,clustering evlove during community splits and data visualization.

# 2.Key features and task involved it: 

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

# 3 Algorithms and Citation
The spectral modularity algorithm is based on the idea that the modularity matrix 𝐵.
B encodes how strongly pairs of nodes are connected compared to what would be expected at random. The key theoretical result of Newman (2006) is that the leading eigenvector of the modularity matrix can be used to find the optimal division of a network into two communities.

# Algorithm Citation:
The spectral modularity method used in this project is based on the foundational work of:
#Newman, M. E. J. (2006).
Modularity and community structure in networks.
Proceedings of the National Academy of Sciences, 103(23), 8577–8582.
This paper introduced the modularity matrix B, proved the eigenvector-based modularity maximization method, and formally established the recursive bisection approach.

# Dataset Citation:
The Karate Club network used in this project originates from:
Zachary, W. W. (1977).
An information flow model for conflict and fission in small groups.
Journal of Anthropological Research, 33(4), 452–473

# 4.How the Algorithm Works in the project:

# 1.Load data

Load the Zachary Karate Club graph (34 nodes, 78 edges).
Keep node IDs and any ground-truth labels (Mr. Hi / President) for evaluation.

# 2.Compute basic graph quantities

Build adjacency matrix A.
Compute degree vector 𝑘 where 𝑘𝑖=∑𝑗𝐴𝑖𝑗ki=∑jAij
Compute number of edges 𝑚=1/2∑𝑖𝑘𝑖m=21∑iki
	​
# 3.Form modularity matrix 
Use formula: 𝐵=𝐴−𝑘𝑘^T/2m
𝐵𝑖𝑗 measures deviation from the degree-preserving random model.

# 4.Compute leading eigenpair of 𝐵
Find largest eigenvalue 𝜆1 and corresponding eigenvector 𝑢1.
Use a symmetric eigensolver (e.g., scipy.sparse.linalg.eigsh or numpy.linalg.eigh).

# 5.Check splitting condition
If 𝜆1≤0: do not split this group (no modularity gain possible).
If λ1>0: proceed to split (there is a positive modularity improvement).

# 6.Bipartition by sign of 𝑢1
For each node i:
Assign to group 𝐶+ if 𝑢1,i>0.
Assign to group 𝐶_ if 𝑢1,𝑖≤0​
This yields a two-way partition for the current group.

# 7.Record results & visualize

Plot the current graph using a fixed layout; color nodes by community.
Label nodes with IDs so changes across iterations are visible.
Compute modularity 
𝑄=1/4𝑚𝑠^T𝐵𝑠 for this split (optional check).

# 8.Compute and store node metrics

After the split, compute for every node:
-Degree centrality
-Betweenness centrality
-Closeness centrality
-Clustering coefficient
Save these metric values indexed by recursion level (iteration).

# 9.Recurse on subcommunities

For each group C produced:

Construct restricted modularity matrix 𝐵(𝐶)(rows/cols only for nodes in C).
Repeat steps 4–8 on C.

# 10.Stopping criterion

Stop recursion on a group when its leading eigenvalue 𝜆1(𝐶)<=0.
When all groups are non-splittable, recursion ends.

# 10.Final outputs to produce
Final partition (list of communities).
Modularity score(s) for final partition.
Visualizations at every split (fixed layout, colored communities).
Time series / evolution plots of each node metric across recursion levels.
Evaluation vs ground truth (ARI, NMI, accuracy) if required.

# 12.Optional refinement

(Optional) Run a local modularity-optimization (e.g., Louvain or greedy) starting from spectral labels to try to improve 𝑄.
Compare refined partition to spectral-only result.

# 5.Summary of Results & Conclusion

# Final Output of the Algorithm

The spectral modularity approach ultimately divided the Karate Club graph into five final communities, achieved through four successful recursive splits. Each split captured progressively finer levels of structure within the social network.

 # Key Insight 1: Structure of the Splits

The first division produced the most meaningful separation, clearly isolating the two well-known factions of the club:
One centered around Node 0 (“Mr. Hi”)the other around Node 33 (“Officer”)
This mirrors the real-life split documented by Zachary.
The later divisions focused on finer substructures: the algorithm detected smaller, tightly connected subgroups inside the two main factions.
Notably, Node 11 emerged as an isolated, singleton-like community, reflecting its unique tie patterns that did not strongly align with either faction.

#  Key Insight 2: Insights from Metric Evolution

The evolution of centrality metrics provided deep behavioral insights into the network.
Betweenness centrality gave the most striking trend:
Initially, Nodes 0 and 33 displayed very high betweenness, showing they acted as bridges across the entire network.
After the first split, their betweenness dropped to nearly zero, indicating that:
Their brokerage roles disappeared.
They became leaders of their own isolated sub-communities rather than connectors across factions.
This demonstrates that a node's structural importance can dramatically shift depending on the community context.

#  Overall Interpretation and Conclusion

This project highlights that node importance is not an intrinsic or fixed characteristic. Instead, a node’s role is context-dependent and changes significantly as the network is decomposed into communities.
By recursively applying the spectral modularity algorithm, the analysis showed:
-How global influencers can become local leaders.
-How tightly knit clusters emerge from broader social groups.
-How certain nodes operate on the periphery and may form standalone communities.
Ultimately, the algorithm demonstrated that network centralities are dynamic measures, reflecting the structural rearrangements that occur when a complex graph is broken down into modular, cohesive components.





