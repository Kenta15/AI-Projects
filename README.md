# AI-Projects
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)

## [A* Algorithm and A* Variant]

### Overview
In this project, we were responsible for implementing A* algorithm and A* variant with heuristic to find a optimal path.
A* is dijkstras algorithm + heuristic(remaining cost to the goal).
Therefore, given dijkstras algorithm, we needed to add a heuristic function.
For A* variant we tried bidirectional search and weighted A*.

### Code Example
```diff
def heuristic(map_, v, goal):

	delta_h = map_.getTile(goal.x, goal.y) - map_.getTile(v.x, v.y)

	if delta_h > 0: 
		dx = abs(v.x - goal.x)
		dy = abs(v.y - goal.y)
		distance = max(dx, dy)
		
		s = (delta_h / distance)
		if s < 1:
			heuristic = math.exp(s) * delta_h # s < 1, delta height is smaller, so cost of each step is smaller.
		else:
			heuristic = math.e * delta_h 

	if delta_h < 0: 
		dx = abs(v.x - goal.x)
		dy = abs(v.y - goal.y)
		distance = max(dx, dy)
		
		s = (delta_h / distance) 
		heuristic = (math.exp(s)  * distance) 

	else:			
		dx = abs(v.x - goal.x)
		dy = abs(v.y - goal.y)
		heuristic = max(dx, dy)


	return heuristic 
```

### Bidirectional search
• Bidirectional search finds a path by dividing the path into two as start to goal and goal to start.

• The heuristic remains the same so the both paths will find a optimal path for each direction.

• Once they meet at the point in the middle, that means we can create a complete path.

### Weighted A*
• Weighted A* just multiplies the heuristic by constant weight

• The heuristic never overestimates the cost but it can underestimate.

• Underestimation may result a lack of efficiency. Thus, we needed to find the right value for the weight.

## [Connect4 Game]

### Overview
Connect4 is a game that you try to coneect 4 pieces in the 6x7 board.
Connection can be made in a row, column, or diagonal.
In this project, we designed an evaluation function to maximize the number of wins against multiple agents.
We implemented a minimax algorithm which maximize our minimum benefit and minimize opponent's maximum benefit.

### Evaluation Function
Our evaluation function is separated by rows, colums, and diagonals.
We add scores if our benefit, and subtract if opponent's benefit.

**[Rows]** - Iterate each row from bottom to top. We count the number of our pieces and zeros until we encounter an opponent piece.
Onece we find an opponent piece, it means our connection is blocked, thus, we calculate the number of our pieces as well as zeros.
If we can make a sequence of 4 out of that, then we add it to the score (a sequence of 3 is higher than a sequence of 2, and more spaces are good). 
If not, we just ignore. If we see all zeros in a row, then break the loop since there is no way to put pieces on top.

**[Columns]** - Iterate each column from the left to the right. For columns, there is no way to have spaces between pieces, so we are only curious if we can make a sequence of 4 with the top most piece in the column. If we find that we can make a sequence of 4 with the top most sequence and all the zeros on the top, then we add it to the score.

**[Diagonal]** - The logic is the same as rows. However, we have diagonals from left to right and right to left. Therefore, we have two loops to find the diagonals.

### Alpha-beta pruning
Alpha-beta pruning is the way to decrease the number of nodes to search that is evaluated by a minimax algorithm.

It increases the maximum deapth that a minimax algorithm can search.



