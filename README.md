# DFS_using_python
Depth first search-returns the first solution it finds, DFS checks for new cycles, DFS might get stuck going down infinite path, even if there are no cycles, DFS is incomplete, DFS also called Backtrack search, In this type of search only one successor is needed at a time, each partially expanded node remembers which successor to generate next.  
import networkx as nx

# Create a directed graph
G = nx.DiGraph()

# Add nodes
nodes = ['S', 'A', 'B', 'C', 'D', 'E', 'G']
G.add_nodes_from(nodes)

# Add edges
edges = [
    ('S', 'A'), ('S', 'B'), ('A', 'D'), ('B', 'C'), ('C', 'E'), ('D', 'G'), ('B', 'A')
]
G.add_edges_from(edges)

# Find all possible paths from 'S' to 'G' using DFS
def find_paths(graph, start, end, path=[]):
    path = path + [start]
    if start == end:
        return [path]
    paths = []
    for neighbor in graph.successors(start):
        if neighbor not in path:
            new_paths = find_paths(graph, neighbor, end, path)
            for new_path in new_paths:
                paths.append(new_path)
    return paths

source = 'S'
goal = 'G'

# Find all possible paths using DFS
all_paths = find_paths(G, source, goal)

# Print all paths
for path in all_paths:
    print(" -> ".join(path))
