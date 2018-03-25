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


**5.16 (3rd edn)**

This question considers pruning in games with chance nodes. This figure shows the complete game tree for a very simple such game. Assume that the leaf nodes are to be evaluated in left-to-right order, and that before a leaf node is evaluated, we know nothing about its value -- the range of possible values is -∞ to ∞.

![image](https://github.com/nvinayvarma189/test/blob/master/images/minmax.jpg)

**(b)**

Given the values of the first six leaves, do we need to evaluate the seventh and eighth leaf? Given the values of the first seven leaves, do we need to evaluate the eighth leaf? Explain your answers.

### Answer

The value of the left branch is 1.5 . After the first six leaves, we still need to keep evaluating, because if the 7th and 8th leaf were both greater than 3 then the right branch would be preferred. Once the 7th leaf is evaluated, we know that the value of the right branch is at most -0.5, so we do not need to evaluate the 8th leaf.

**(C)**

Suppose the leaf node values are known to lie between -2 and 2 inclusive. After the first two leaves are evaluated, what is the value range for the left-hand chance node?

### Answer

It is between 0 and 2 (inclusive).

**(d)**

### Answer

Only the first five leaves need to be evaluated. After that, we know that the right branch is between -2 and 1, so it is definitely inferior to the left branch.


**6.13 (2nd edn)**

The Chinook checkers program makes extensive use of endgame databases, which provide exact values for every position with eight or fewer pieces. How might such databases be efficiently generated, stored and accessed?


### Answer

An indexing function can be found which assigns a unique number to each position, and classifies the positions into "slices", based on the number of kings and checkers, and the rank of the most advanced checker, for each colour. These different "slices" of the database can be compressed and decompressed as needed during a game. The Chinook database contains 443,748,401,247 positions, but compresses into roughly 6 gigabytes.


The database is essentially a gigantic lookup table, whose values can be generated by a technique known as "Retrograde Analysis". We assume inductively that all positions with N-1 or fewer pieces have been evaluated, before extending to positions with N pieces. Positions with a forced capture are evaluated first (because they lead directly to a position with fewer pieces). The remaining positions can be labeled using either a "forward" or "backward" approach. The "forward" approach looks at an unlabeled position and generates all possible successor positions. The "backward" approach looks at a labeled position and generates all possible predecessor positions. We keep looping through the remaining positions until we get through a loop with no new positions being labeled. It follows that all remaining unlabeled positions must result in a draw.Details can be found [here](http://www.cs.ualberta.ca/~chinook/publications)

## Question (misc)

Decision Trees

Consider the collection of examples:

height:	short, tall

hair:	dark, red, blond

eyes:	blue, brown

% +

short	blond	blue

tall	red	blue

tall	blond	blue

% -

tall	blond	brown

short	dark	blue

tall	dark	blue

tall	dark	brown

short	blond	brown

Use entropy to choose the best attribute for the first split in a decision tree to classify objects as belonging to the class, + or -.

### Answer

There are 3 objects in class '+' and 5 in '-', so the entropy is:
Entropy(parent) = Σi Pi log2Pi = -(3/8)log(3/8) - (5/8)log(5/8) = 0.954

Suppose we split on height:

![image](https://github.com/nvinayvarma189/test/blob/master/images/decision.jpg)


Of the 3 'short' items, 1 is '+' and 2 are '-', so Entropy(short) = -(1/3)log(1/3) - (2/3)log(2/3) = 0.918

Of the 5 'tall' items, 2 are '+' and 3 are '-', so Entropy(tall) = -(2/5)log(2/5) - (3/5)log(3/5) = 0.971

The average entropy after splitting on 'height' is Entropy(height) = (3/8)(0.918) + (5/8)(0.971) = 0.951

The information gained by testing this attribute is: 0.954 - 0.951 = 0.003 (i.e. very little)

If we try splitting on 'hair' we find that the branch for 'dark' has 3 items, all '-' and the branch for 'red' has 1 item, in '+'. Thus, these branches require no further information to make a decision. The branch for 'blond' has 2 '+' and 2 '-' items and so requires 1 bit. That is,

Entropy(hair) = (3/8)(0) + (1/8)(0) + (4/8)(1) = 0.5

and the information gained by testing hair is 0.954 - 0.5 = 0.454 bits.

By a similar calculation, the entropy for testing 'eyes' is (5/8)(0.971) + (3/8)(0) = 0.607, so the information gained is 0.954 - 0.607 = 0.347 bits.

Thus 'hair' gives us the maximum information gain.

Since the 'blond' branch for hair still contains a mixed population, we would apply the whole procedure recursively on the population remaining in the 'blond' branch. Note that we now only need to test 'height' and 'eyes' since the 'hair' attribute has already been used.

## N-Queens Question

Consider the following state for the 8-queens problem:

![image](https://github.com/nvinayvarma189/test/blob/master/images/nqueens.jpg)

## (a)

is this a solution?

### Answer

No, the queens on columns 2 and 5 are attacking each other.

## (b)

what is the value of h?

### Answer

There is only one violation, so h=1.

## (c)

explain why Hill-climbing with Min Conflicts would get stuck in this state, but Simulated Annealing may be able to "escape" and eventually find a solution.

### Answer

For each column, moving the queen on that column (while keeping the other queens in place) would result in an increase to h. Therefore, any such move will be rejected by Hill-climbing. Simulated Annealing, however, can accept such a move with probability exp(-(h1-h0)/T), thus bumping the system out of this local optimum and allowing it to continue the search for a global optimum.
