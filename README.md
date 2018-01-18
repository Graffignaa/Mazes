Maze Game

Options for generating maze:
- Kruskal's algorithm

Options for solving maze: 
- BFS
- DFS
- Fast BFS
- Distance-colored Fast BFS (the trippiest one). Solves maze with Fast BFS
	while coloring each node by its distance from the start as well.
	* The coloring of nodes will change as the solving progresses into the
	maze, because rainbow is colored by the node's distance from the end of
	the solved area. There is always a full rainbow and exactly a full rainbow
	represented by the drawn nodes.
- Player solves by hand - Use arrow keys to move, you are the black square.
- "Solving" by rendering each node's distance from start with color
- Solver FIGHT: A normal DFS and an normal BFS solve the maze at the same time.
	The DFS is rendered in red, the BFS in blue, and their overlap in purple.
	When one algorithm wins, the finished path is rendered in either dark
	red or dark blue (depending on which solver wins).

Full list of extra (credit) features:
- Fast Breadth-First Search algorithm
- Maze coloration by depth (the further along the rainbow, the deeper in
	the maze) 
- Ability to toggle color viewing
- Option to "give up" when solving maze manually, using an algorithm to finish
	(I still haven't solved one of the 100x60 ones by hand....-suzanne)
- Various menus detailing all available options in the game at any point
- Option to reset/get new maze at any point


Classes

In file Maze.java:

Node
A node (vertex) in the graph, has 0-4 edges. Has methods that check for
and return neighbor nodes and edges, and to render the node w/given color.
Has grid coordinates that are used for rendering and also to identify it and
compare to other nodes. Node equality determined with .equals() (no override)

EndNode
Subclass of Node. Only the node in the bottom right corner of the graph
is of this class (it's always constructed last in the randomEdges method 
in Maze).

Edge
An edge in the graph, connects two edges. Can be constructed w/ random or 
given edge weight.

Maze
Contains a graph of nodes and edges of variable size. 
Has methods that:
- Initialize the grid-shaped graph of nodes and edges
- Sort all edges by weight
- Initialize map of nodes to themselves as representatives
- Create the spanning tree (and reassign representatives in the map)
- Remove edges that are not in spanning tree from all nodes (those edges still
exist, but the nodes no longer store any reference to them)
HashMap is Node to Node.

In file Solver.java:

ASolver (extended by all the following classes)
An abstract class for maze solvers. Stores fields common to all solvers, as
well as the path reconstruct method and a HashMap of Node to Edge used to
reconstruct path, and a standard render method. 

DFSSolver, BFSSolver, FastBFSSolver
Implement step() differently to follow their various algorithms. FastBFSSolver
stores an ArrayList of paths instead of just one path.

Player
Implements step(String ke) and not step(), and stores Node location of player
in the maze.

ColorMazeFromStart
The step() method goes ahead and "solves" the whole maze in one invocation,
assigning each node to an integer value representing its distance from the
start of the maze (along a path in the maze, not by grid coordinates). It's
colored according to the rainbow, pink -> red -> orange -> ... blue -> purple,
and overrides .renderOnto from ASolver
Sometimes I open the game, generate the rainbow, and just stare at it for
minutes on end. It takes the pain of testing away, if only for a moment. 
