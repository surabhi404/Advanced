# SIX CLASSES OF ALGOS:

Centrality

Classification

Community

Node Embeddings

Path

Similarity

## Centrality Algorithms
Centrality algorithms find the important vertices in a graph based on their connections with other vertices. A centrality algorithm usually assigns scores to vertices or edges based on how close they are to the center of connection-based activity.

Approximate Closeness Centrality
tg_closeness_approx (
SET v_type,
SET e_type,
INT k = 100, # sample num
INT max_hops = 10, # max BFS explore steps
DOUBLE epsilon = 0.1, # error parameter
BOOL print_accum = true, # output to console
STRING file_path = "", # output file
INT debug = 0, # debug flag -- 0: No LOG;1: LOG without the sample-node bfs loop;2: ALL LOG.
INT sample_index = 0, # random sample group
INT maxsize = 1000, # max size of connected components using exact closeness algorithm
BOOL wf = True # Wasserman and Faust formula
)

Betweenness Centrality
The Betweenness Centrality of a vertex is defined as the number of shortest paths that pass through this vertex, divided by the total number of shortest paths. That is

BC(v)=∑s≠v≠tPDst(v)=∑s≠v≠tSPst(v)/SPst,
where PDis called the pair dependency, SPstis the total number of shortest paths from node s to node t and SPst(v)is the number of those paths that pass through v.

CREATE QUERY tg_betweenness_cent(SET v_type, SET e_type,
STRING re_type,INT max_hops=10, INT top_k=100, BOOL print_accum = True,
STRING result_attr = "", STRING file_path = "", BOOL display_edges = FALSE)

Degree Centrality
Degree centrality is defined as the number of edges incident upon a vertex (i.e., the number of ties that a node has). The degree can be interpreted in terms of the immediate risk of a node for catching whatever is flowing through the network (such as a virus, or some information).

CREATE QUERY tg_degree_cent(SET v_type, SET e_type,
SET re_type, BOOL in_degree = TRUE, BOOL out_degree = TRUE,
INT top_k=100, BOOL print_accum = True, STRING result_attr = "",
STRING file_path = "")

## Classification Algorithms
Classification algorithms assign a label (class name) to a vertex based on it satisfying the established conditions for membership in that class. This differs from community (or clustering) algorithms in which there are no pre-established conditions for membership.

Greedy Graph Coloring
This algorithm assigns a unique integer value known as its color to the vertices of a graph such that no neighboring vertices share the same color. The reason why this is called color is that this task is equivalent to assigning a color to each nation on a map so that no neighboring nations share the same color.

CREATE QUERY tg_greedy_graph_coloring(SET v_type,SET e_type, UINT max_colors = 999999,BOOL print_color_count = TRUE, BOOL display = TRUE, STRING file_path = "")

k-Nearest Neighbors
The k-Nearest Neighbors (kNN) algorithm is one of the simplest classification algorithms. It assumes that some or all the vertices in the graph have already been classified. The classification is stored as an attribute called the label. The goal is to predict the label of a given vertex, by seeing what are the labels of the nearest vertices.

tg_knn_cosine_ss (VERTEX source, SET v_type, SET e_type, SET
re_type, STRING weight, STRING label, INT top_k,
BOOL print_accum = TRUE, STRING file_path = "", STRING attr = "")
RETURNS (STRING)

k-Nearest Neighbors (Cross-Validation Version)
ou can choose the value for topK based on your experience, or using cross-validation to optimize the hyperparameters. In our library, Leave-one-out cross-validation for selecting optimal k is provided

tg_knn_cosine_cv(SET v_type, SET e_type, SET re_type,
STRING weight, STRING label, INT min_k, INT max_k) RETURNS (INT)

## Community Algorithms
Community algorithms group together vertices or edges that satisfy some rule for being connected to one another. Community algorithms are different from classification algorithms because classification does not necessarily consider connections

K-Core Decomposition
A k-core of a graph is a maximal connected subgraph in which every vertex is connected to at least k vertices in the subgraph. To obtain the k-core of a graph, the algorithm first deletes the vertices whose outdegree is less than k

tg_kcore(STRING v_type, STRING e_type, INT k_min = 0, INT k_max = -1,
BOOL print_accum = TRUE, STRING attr = "", STRING file_path = "",
BOOL show_membership = FALSE, BOOL show_shells=FALSE)

Label Propagation
Label Propagation is a heuristic method for determining communities. The idea is simple: If the plurality of your neighbors all bear the label X, then you should label yourself as also a member of X. The algorithm begins with each vertex having its own unique label.

tg_label_prop (SET v_type, SET e_type, INT max_iter, INT output_limit,
BOOL print_accum = TRUE, STRING file_path = "", STRING attr = "")

Local Clustering Coefficient
The Local Clustering Coefficient algorithm computes the local clustering coefficient of every vertex in a graph. The local clustering coefficient of a vertex (node) in a graph quantifies how close its neighbors are to being a complete graph, where every two distinct vertices are connected by an edge. It is obtained by dividing the number edges between a vertex’s neighbors by the number of edges that could possibly exist

tg_lcc(STRING v_type, STRING e_type,INT top_k=100,
BOOL print_accum = True, STRING result_attr = "",
STRING file_path = "", BOOL display_edges = FALSE)
## Similarity
JACCARD SIMILARITY

COSINE SIMILARITY

GRAPH BASED VARIATIONS
