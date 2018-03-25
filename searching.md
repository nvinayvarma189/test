Romania map search

### Some definitions:

**State space:** set of cities on Romania Map
Successor function: s(x) is the set of cities adjacent to x on the map

**Goal state:** Bucharest

**Path cost:** sum of the costs of distances between the cities on the path

*Output for runnig these algorithms on Romania:*

**(BFS)** = Arad, Sibiu, Timisoara, Zerind, Fagaras, Oradea, Rimnicu Vilcea, Lugoj, Bucharest.

**(UCS)** = Arad(0), Zerind(75), Timisoara(118), Sibiu(140), Oradea(146), Rimnicu Vilcea(220), Lugoj(229), Fagaras(239), Mehadia(299), Pitesti(317), Craiova (366), Dobreta (374), Bucharest (418).

**(DFS)** = Arad, Sibiu, Fagaras, Bucharest. Note that the solution is found quickly only because of the rule for ordering the successors alphabetically; this is not usually the case! If the nodes were ordered differently, we could end up taking a much longer path.

**(IDS)** = Arad; Arad, Sibiu, Timisoara, Zerind; Arad, Sibiu, Fagaras, Oradea, Rimnicu Vilcea, Timisoara, Lugoj, Zerind, Oradea; Arad, Sibiu, Fagaras, Bucharest.

**(Greedy)** = Arad (366), Sibiu (253), Fagaras (178), Bucharest (0).

**(A*Search)** = Arad(0+366=366), Sibiu(140+253=393), Rimnicu Vilcea(220+193=413), Pitesti(317+98=415), Fagaras(239+178=417), Bucharest(418+0=418).

**(DFS with reverse alphabetical order)** = Arad, Zerind, Oradea, Sibiu, Rimnicu Vilcea, Pitest, Craiova, Dobreta, Mehadia, Lugoj, Timisoara, Bucharest.

## Question

**3.18 (3rd edn)**

### (a)
Describe a search space in which Iterative Deepening Search performs much worse than          Depth-First Search.

### Answer
This will be true in search spaces with very low branching factor. As an extreme example, consider a problem with a branching factor of 1 at every move, and a solution at depth n.   Depth-First Search will take exactly n expansions to find a solution, while Iterative Deepening Search will take O(n2).

**3.18 (2nd edn)**

### (b) (add)
Describe a search space in which Breadth-First Search performs much worse than Depth-First Search.

### Answer
A search problem where there exist many solutions at a fairly deep level, such that DFS will find a solution more or less as soon as it gets to that depth for the first time. For example, imagine you are shipwrecked in the middle of a lake and you need to find a path to the shoreline, with a series of small steps either up, down, left or right. DFS will find a path quickly, whereas BFS will spend a lot of time exploring all paths shorter than the radius of the lake.

![image](https://github.com/nvinayvarma189/test/blob/master/images/space.jpg)

### (c) (add)
Describe a search space in which Depth-First Search performs much worse than Breadth-First Search.

### Answer
A search problem where the search depth is large or even unlimited, but a solution can be found at a very shallow depth. BFS will find the shallow solution quickly while DFS will get "lost" in the first path it explores.

## Question

**3.21 (3rd edn)**

**Prove each of the following statements:**

### (a)

Breadth First Search is a special case of Uniform Cost Search

### Answer
Uniform Cost Search reduces to Breadth First Search when all edges have the same cost.

### (b)
Breadth First Search, Depth First Search and Uniform Cost Search are special cases of best-first search.

### Answer
best-first search reduces to Breadth-First Search when f(n) = number of edges from start node to n, to UCS when f(n) = g(n);
it can be reduced to DFS by, for example, setting f(n) = -g(n) (thus forcing deep nodes on the current branch to be searched before shallow nodes on other branches).

### (c)

Uniform Cost Search is a special case of A*Search

### Answer
A*Search reduces to UCS when the heuristic function is zero everywhere, i.e. h(n) = 0 for all n;
this heuristic is clearly admissible since it always (grossly!) underestimates the distance remaining to reach the goal.

## Question
**3.25 (3rd edn)**

The **heuristic path algorithm** is a best-first search in which the objective function is
f(n) = (2-w)g(n) + wh(n)

For what values of w is this algorithm complete? For what values of w is it optimal, assuming h() is admissible?
What kind of search does this perform when w=0? when w=1? when w=2?

### Answer
This algorithm reduces to Uniform Cost Search when w=0, to A*Search when w=1 and to Greedy Search when w=2.
It is guaranteed to be optimal when 0 ≤ w ≤ 1, because it is equivalent to A*Search using the heuristic

h'(n) = [w/(2-w)]h(n) ≤ h(n)

When w > 1 it is not guaranteed to be optimal (however, it might work very well in practice, for some problems).

**8-Puzzle problem**

Consider the following arrangement of tiles in the 8-puzzle:

  1	2	3
  
  8	5		
  
  4	7	6
  
Keeping in mind that the goal state is:

  1	2	3
  
  4	5	6
  
  7	8		
  
Trace the A*Search algorithm using the Total Manhattan Distance heuristic, to find the shortest path from the initial state shown above, to the goal state.

![image](https://github.com/nvinayvarma189/test/blob/master/images/8queens.jpg)

Note: The algorithm begins by exploring the left branch which, according to the heuristic, seems the most promising. After a few steps the heuristic for the left branch starts to exceed that of middle branch, so exploration shifts to the middle branch, where the optimal solution is ultimately found.

## Question

**5.9 (3rd edn)**

This problem exercises the basic concepts of game playing, using tic-tac-toe (naughts and crosses) as an example. We define Xn as the number of rows, columns or diagonals with exactly n X's and no O's. Similarly, On is the number of rows, columns or diagonals with just n O's. The utility function assigns +10 to any position with X3>=1 and -10 to any position with O3>=1. All other terminal positions have utility 0. For the nonterminal positions, we use a linear evaluation function defined as Eval(s) = 3X2(s) + X1(s) - (3O2(s) + O1(s))

**(a)**
Approximately how many possible games of tic-tac-toe are there?

### Answer

There are 9 choices for the 1st move, 8 for the 2nd move, 7 for the 3rd move, etc., giving us an upper bound of 9! = 9*8*7*6*5*4*3*2*1 = 362880. But this is an overestimate, because some games end in 5, 6, 7 or 8 moves. The true figure is actually 255168.

If we take symmetry into account, the number reduces substantially. For example, there are now only 3 choices for the first move and at most 5 choices for the second move. In fact, the total is reduced to 26830 distinct games, of which 172 end in 5 moves, 579 end in 6 moves, 5115 end in 7 moves, 7426 end in 8 moves, 8670 result in a win in 9 moves and 4868 result in a draw. There are a number of Web sites providing a full analysis. See for example [here](http://www.se16.info/hgb/tictactoe.htm)

**(b)**

Show the whole game tree starting from an empty board down to depth 2 (i.e. one X and one O on the board), taking symmetry into account.

**(c)**

Mark on your tree the evaluations of all the positions at depth 2.

**(d)**

Using the minimax algorithm, mark on your tree the backed-up values for the positions at depths 1 and 0, and use those values to choose the best starting move.

**(e)**

Circle the nodes at depth 2 that would not be evaluated if alpha-beta pruning were applied, assuming the nodes are generated in the optimal order for alpha-beta pruning.

### Answer 

![image](https://github.com/nvinayvarma189/test/blob/master/images/tictactoe.jpg)

**6.13 (2nd edn)**

The Chinook checkers program makes extensive use of endgame databases, which provide exact values for every position with eight or fewer pieces. How might such databases be efficiently generated, stored and accessed?


### Answer

An indexing function can be found which assigns a unique number to each position, and classifies the positions into "slices", based on the number of kings and checkers, and the rank of the most advanced checker, for each colour. These different "slices" of the database can be compressed and decompressed as needed during a game. The Chinook database contains 443,748,401,247 positions, but compresses into roughly 6 gigabytes.


The database is essentially a gigantic lookup table, whose values can be generated by a technique known as "Retrograde Analysis". We assume inductively that all positions with N-1 or fewer pieces have been evaluated, before extending to positions with N pieces. Positions with a forced capture are evaluated first (because they lead directly to a position with fewer pieces). The remaining positions can be labeled using either a "forward" or "backward" approach. The "forward" approach looks at an unlabeled position and generates all possible successor positions. The "backward" approach looks at a labeled position and generates all possible predecessor positions. We keep looping through the remaining positions until we get through a loop with no new positions being labeled. It follows that all remaining unlabeled positions must result in a draw.Details can be found [here](http://www.cs.ualberta.ca/~chinook/publications)


