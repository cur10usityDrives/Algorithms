# Maze Solver Project

## Overview
This project focuses on solving maze problems using two classic graph traversal techniques: 
Depth-First Search (DFS) and Breadth-First Search (BFS). 
The goal is to determine if a path exists from a start position to a destination within a 2D grid maze. 
The project is implemented in Python and tested with various maze configurations from LeetCode.

## Introduction
Maze solving is a common problem in computer science, often used to teach graph traversal algorithms. This project employs DFS and BFS to navigate through a maze represented as a 2D grid. Each algorithm offers unique advantages and trade-offs, which are explored through their implementation and performance analysis.

## Design and Implementation

### Depth-First Search (DFS)
DFS is an algorithm that starts at the root (or an arbitrary node) and explores as far as possible along each branch before backtracking. 

**Key Components:**
- **Recursive Approach:** DFS is implemented recursively to traverse the maze.
- **Backtracking:** When a dead end is reached, the algorithm backtracks to explore alternative paths.
- **Memory Efficiency:** DFS uses less memory as it stores only the current path.

**Implementation:**
```python
def hasPath(maze, start, destination) -> bool:
    if not maze:
        return False
    m, n = len(maze), len(maze[0])
    visited = set()

    def dfs(x, y):
        if [x, y] == destination:
            return True
        if (x, y) in visited:
            return False
        visited.add((x, y))
        directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]
        for dx, dy in directions:
            newX, newY = x, y
            while 0 <= newX + dx < m and 0 <= newY + dy < n and maze[newX + dx][newY + dy] == 0:
                newX += dx
                newY += dy
            if dfs(newX, newY):
                return True
        return False

    return dfs(start[0], start[1])
```

### Breadth-First Search (BFS)
BFS is an algorithm that starts at the root (or an arbitrary node) and explores all neighbors at the present depth prior to moving on to nodes at the next depth level.

**Key Components:**
- **Queue Data Structure:** BFS uses a queue to manage the traversal.
- **Shortest Path Guarantee:** Due to its level-wise exploration, BFS finds the shortest path first.
- **Higher Memory Usage:** BFS can use more memory as it needs to store all nodes at the current level.

**Implementation:**
```python
from collections import deque

def hasPath(maze, start, destination) -> bool:
    if not maze or not maze[0]:
        return False
    rows, cols = len(maze), len(maze[0])
    visited = set()
    queue = deque([tuple(start)])
    directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]

    while queue:
        i, j = queue.popleft()
        if [i, j] == destination:
            return True
        if (i, j) in visited:
            continue
        visited.add((i, j))
        for dx, dy in directions:
            x, y = i, j
            while 0 <= x + dx < rows and 0 <= y + dy < cols and maze[x + dx][y + dy] == 0:
                x += dx
                y += dy
            if (x, y) not in visited:
                queue.append((x, y))
    return False
```

## Testing
The algorithms are tested using a variety of test cases from LeetCode to ensure correctness and performance. 
Each test case checks if there is a valid path from the start to the destination in different maze configurations.

## Enhancement Ideas
- **Optimized Memory Usage:** Implement iterative DFS to reduce the overhead of recursive function calls.
- **Bidirectional BFS:** Implementing bidirectional BFS can reduce the search space and improve performance.
- **Heuristics:** Incorporate heuristic methods, such as the A* algorithm, to enhance pathfinding efficiency.
- **Parallelization:** Divide the maze into smaller sections and solve them in parallel to speed up maze traversal.

## Conclusion
This project demonstrates the practical applications of DFS and BFS in solving maze navigation problems. 
While DFS is more memory-efficient, BFS guarantees the shortest path, making it suitable for different scenarios. 
Understanding these algorithms provides valuable problem-solving skills for various computational tasks.

## Author
Natnael Haile
