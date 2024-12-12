- **BFS**: **Unweighted** graph, **single source to all nodes**.
- **Dijkstra**: **Weighted** graph, **single source to a target** node.
- **Floyd-Warshall**: **Weighted** graph, **all-pairs shortest paths** between all nodes.
- Negative Weight Edges (Single Source to All Nodes), **Solution**: **Bellman-Ford Algorithm**.
	- **Scenario**: The graph contains **negative edge weights**, and you want to find the shortest path from a **single source node** to all other nodes.
- Graph with Negative Weight Cycles (All-Pairs Shortest Paths). **Solution**: **Floyd-Warshall Algorithm** with cycle detection
	- **Scenario**: The graph contains **negative weight cycles**, and you need to find the shortest paths between all pairs of nodes.
	- **Solution**: Floyd-Warshall can detect negative weight cycles during its execution. If a cycle is detected (i.e., `distance[i][i] < 0` for any node `i`), it indicates the presence of a negative weight cycle.
- Unweighted Graph, Single Source to a Target Node, **Solution**: (DFS or BFS).
	- **Scenario**: You have an **unweighted graph** and you need to find a **single path from a source to a target** node.
- Graph with Multiple Sources, **Solution**: **Dijkstra’s Algorithm (Multi-Source)**
	- You can modify Dijkstra’s algorithm to handle multiple source nodes by initializing the distances for all sources to 0 and then running the algorithm normally.
	- **Alternative**: **Bellman-Ford** can also be used if negative weights are involved, by running the algorithm from each source.
- Graph with Multiple Targets, Shortest Paths from All Nodes
	- **Scenario**: You have a **weighted graph** and need to find the shortest path from **every node** to a specific set of target nodes.
	  
https://chatgpt.com/share/673ee029-e388-8008-9153-2a541b70a878
