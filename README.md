# AI

     #TOWER OF HANOI
            def TowerOfHanoi(n, start_rod, end_rod, transition_rod):
              ## base case for only one disc remaining
              if n==1:
                print("Move disk 1 from rod",start_rod,"to rod",end_rod)
                return
              ## Recursive call for to move the top disc in a stack of 2
              TowerOfHanoi(n-1, start_rod, transition_rod, end_rod)

              print("Move disk",n,"from rod",start_rod,"to rod",end_rod)
              ## Recursive call for to move the top disc in a stack of 3
              TowerOfHanoi(n-1, transition_rod, end_rod, start_rod)
               n = 3
              TowerOfHanoi(n,'A','C','B')

             OUTPUT:
              
              Move disk 1 from rod A to rod C
              Move disk 2 from rod A to rod B
              Move disk 1 from rod C to rod B
              Move disk 3 from rod A to rod C
              Move disk 1 from rod B to rod A
              Move disk 2 from rod B to rod C
              Move disk 1 from rod A to rod C
---------------------------------------------------------------------------------------------------------------------------------------------

    #BFS
              graph = {
                '5' : ['3','7'],
                '3' : ['2', '4'],
                '7' : ['8'],
                '2' : [],
                '4' : ['8'],
                '8' : []
              }

              visited = [] # List for visited nodes.
              queue = []     #Initialize a queue

              def bfs(visited, graph, node): #function for BFS
                  visited.append(node)
                  queue.append(node)

                  while queue:          # Creating loop to visit each node
                  m = queue.pop(0) 
                  print (m, end = " ") 

                  for neighbour in graph[m]:
                      if neighbour not in visited:
                      visited.append(neighbour)
                      queue.append(neighbour)

              # Driver Code
              print("Following is the Breadth-First Search")
              bfs(visited, graph, '5')    # function calling
              
              OUTPUT:
              Following is the Breadth-First Search
              5 3 7 2 4 8 
              
 -----------------------------------------------------------------------------------------------------------------------------------------------------    
 
      #DFS
              graph = {
                '5' : ['3','7'],
                '3' : ['2', '4'],
                '7' : ['8'],
                '2' : [],
                '4' : ['8'],
                '8' : []
              }

              visited = set() # Set to keep track of visited nodes of graph.

              def dfs(visited, graph, node):  #function for dfs 
                  if node not in visited:
                      print (node)
                      visited.add(node)
                      for neighbour in graph[node]:
                          dfs(visited, graph, neighbour)

              # Driver Code
              print("Following is the Depth-First Search")
              dfs(visited, graph, '5')
              
              OUTPUT:
              Following is the Depth-First Search
              5
              3
              2
              4
              8
              7
----------------------------------------------------------------------------------------------------------------------------------------------------------------
      #Best first search
                               from queue import PriorityQueue
                              import matplotlib.pyplot as plt
                              import networkx as nx

                              # for implementing BFS | returns path having lowest cost
                              def best_first_search(source, target, n):
                                  visited = [0] * n
                                  visited[source] = True
                                  pq = PriorityQueue()
                                  pq.put((0, source))
                                  while pq.empty() == False:
                                      u = pq.get()[1]
                                      print(u, end=" ") # the path having lowest cost
                                      if u == target:
                                          break
                                      for v, c in graph[u]:
                                          if visited[v] == False:
                                              visited[v] = True
                                              pq.put((c, v))
                                  print()     
                              # for adding edges to graph
                              def addedge(x, y, cost):
                                  graph[x].append((y, cost))
                                  graph[y].append((x, cost))    
                              v = int(input("Enter the number of nodes: "))
                              graph = [[] for i in range(v)] # undirected Graph
                              e = int(input("Enter the number of edges: "))
                              print("Enter the edges along with their weights:")
                              for i in range(e):
                                  x, y, z = list(map(int, input().split()))
                                  addedge(x, y, z)
                              source = int(input("Enter the Source Node: "))
                              target = int(input("Enter the Target/Destination Node: "))
                              print("Path: ", end = "")
                              best_first_search(source, target, v) 
                              
                OUTPUT:
                    Enter the number of nodes: 4
                    Enter the number of edges: 5
                    Enter the edges along with their weights:
                    0 1 1 
                    0 2 1
                    0 3 2
                    2 3 2
                    1 3 3
                    Enter the Source Node: 2 
                    Enter the Target/Destination Node: 1
                    Path: 2 0 1 
-----------------------------------------------------------------------------------------------------------------------------------------------------

    #tic tac
                     import numpy as np
                    import random
                    from time import sleep

                    def create_board():
                        return(np.array([[0, 0, 0],
                                  [0, 0, 0],
                                [0, 0, 0]]))

                    def possibilities(board):
                        l = []

                        for i in range(len(board)):
                            for j in range(len(board)):

                                if board[i][j] == 0:
                                    l.append((i, j))
                        return(l)

                    def random_place(board, player):
                        selection = possibilities(board)
                        current_loc = random.choice(selection)
                        board[current_loc] = player
                        return(board)

                    def row_win(board, player):
                        for x in range(len(board)):
                            win = True

                            for y in range(len(board)):
                                if board[x, y] != player:
                                    win = False
                                    continue

                            if win == True:
                                return(win)
                        return(win)

                    def col_win(board, player):
                        for x in range(len(board)):
                            win = True

                            for y in range(len(board)):
                                if board[y][x] != player:
                                    win = False
                                    continue

                            if win == True:
                                return(win)
                        return(win)

                    def diag_win(board, player):
                        win = True
                        y = 0
                        for x in range(len(board)):
                            if board[x, x] != player:
                                win = False
                        if win:
                            return win
                        win = True
                        if win:
                            for x in range(len(board)):
                                y = len(board) - 1 - x
                                if board[x, y] != player:
                                    win = False
                        return win

                    def evaluate(board):
                        winner = 0

                        for player in [1, 2]:
                            if (row_win(board, player) or
                                col_win(board,player) or
                                diag_win(board,player)):
                                winner = player
                        if np.all(board != 0) and winner == 0:
                                winner = -1

                        return winner
                    def play_game():
                        board, winner, counter = create_board(), 0, 1
                        print(board)
                        sleep(2)

                        while winner == 0:
                            for player in [1, 2]:
                                board = random_place(board, player)
                                print("Board after " + str(counter) + " move")
                                print(board)
                                sleep(2)
                                counter += 1
                                winner = evaluate(board)
                                if winner != 0:
                                    break
                        return(winner)
                    print("Winner is: " + str(play_game()))
                 
                 OUTPUT:
                     [[0 0 0]
                     [0 0 0]
                     [0 0 0]]
                    Board after 1 move
                    [[0 0 0]
                     [0 0 0]
                     [1 0 0]]
                    Board after 2 move
                    [[0 0 0]
                     [0 0 0]
                     [1 0 2]]
                    Board after 3 move
                    [[0 1 0]
                     [0 0 0]
                     [1 0 2]]
                    Board after 4 move
                    [[0 1 0]
                     [2 0 0]
                     [1 0 2]]
                    Board after 5 move
                    [[0 1 0]
                     [2 0 1]
                     [1 0 2]]
                    Board after 6 move
                    [[0 1 0]
                     [2 2 1]
                     [1 0 2]]
                    Board after 7 move
                    [[0 1 0]
                     [2 2 1]
                     [1 1 2]]
                    Board after 8 move
                    [[2 1 0]
                     [2 2 1]
                     [1 1 2]]
                    Winner is: 2
-------------------------------------------------------------------------------------------------------------------------------------------------

       #WaterJugProblem
       
                    from collections import defaultdict
                    jug1, jug2, aim = 4, 3, 2
                    visited = defaultdict(lambda: False)
                    def waterJugSolver(amt1, amt2):
                        if (amt1 == aim and amt2 == 0) or (amt2 == aim and amt1 == 0):
                            print(amt1, amt2)
                            return True
                        if visited[(amt1, amt2)] == False:
                            print(amt1, amt2)
                            visited[(amt1, amt2)] = True
                            return (waterJugSolver(0, amt2) or
                            waterJugSolver(amt1, 0) or
                            waterJugSolver(jug1, amt2) or
                            waterJugSolver(amt1, jug2) or
                            waterJugSolver(amt1 + min(amt2, (jug1-amt1)),
                            amt2 - min(amt2, (jug1-amt1))) or
                            waterJugSolver(amt1 - min(amt1, (jug2-amt2)),
                            amt2 + min(amt1, (jug2-amt2))))
                        else:
                            return False

                    print("Steps: ")
                    waterJugSolver(0, 0)
                    
                    OUTPUT:
                     
                       Steps: 
                              0 0
                              4 0
                              4 3
                              0 3
                              3 0
                              3 3
                              4 2
                              0 2
                              True
 -------------------------------------------------------------------------------------------------------------------------------------------------------
     #Travelling Salesman problem
    
                     import copy
                    from heapq import heappush, heappop
                    n = 3
                    row = [ 1, 0, -1, 0 ]
                    col = [ 0, -1, 0, 1 ]

                    class priorityQueue:
                        def __init__(self):
                            self.heap = []
                        def push(self, k):
                             heappush(self.heap, k)
                        def pop(self):
                            return heappop(self.heap)
                        def empty(self):
                            if not self.heap:
                                return True
                            else:
                                return False

                    class node:
                            def __init__(self, parent, mat, empty_tile_pos,cost, level):
                                self.parent = parent
                                self.mat = mat
                                self.empty_tile_pos = empty_tile_pos
                                self.cost = cost
                                self.level = level

                            def __lt__(self, nxt):
                                return self.cost < nxt.cost
                    def calculateCost(mat, final) -> int:
                        count = 0
                        for i in range(n):
                            for j in range(n):
                                if ((mat[i][j]) and (mat[i][j] != final[i][j])):
                                    count += 1
                        return count

                    def newNode(mat, empty_tile_pos, new_empty_tile_pos,level, parent, final) -> node:
                        new_mat = copy.deepcopy(mat)
                        x1 = empty_tile_pos[0]
                        y1 = empty_tile_pos[1]
                        x2 = new_empty_tile_pos[0]
                        y2 = new_empty_tile_pos[1]
                        new_mat[x1][y1], new_mat[x2][y2] = new_mat[x2][y2], new_mat[x1][y1]
                        cost = calculateCost(new_mat, final)
                        new_node = node(parent, new_mat, new_empty_tile_pos,cost, level)
                        return new_node

                    def printMatrix(mat):
                        for i in range(n):
                            for j in range(n):
                                print("%d " % (mat[i][j]), end = " ")
                            print()

                    def isSafe(x, y):
                        return x >= 0 and x < n and y >= 0 and y < n

                    def printPath(root):
                        if root == None:
                            return
                        printPath(root.parent)
                        printMatrix(root.mat)
                        print()

                    def solve(initial, empty_tile_pos, final):
                        pq = priorityQueue()
                        cost = calculateCost(initial, final)
                        root = node(None, initial,empty_tile_pos, cost, 0)
                        pq.push(root)
                        while not pq.empty():
                            minimum = pq.pop()
                            if minimum.cost == 0:
                                printPath(minimum)
                                return
                            for i in range(n):
                                new_tile_pos = [minimum.empty_tile_pos[0] + row[i],minimum.empty_tile_pos[1] + col[i], ]
                                if isSafe(new_tile_pos[0], new_tile_pos[1]):
                                    child=newNode(minimum.mat,minimum.empty_tile_pos,new_tile_pos,minimum.level+1,minimum,final,)
                                    pq.push(child)
                    initial = [ [ 1, 2, 3 ],[ 5, 6, 0 ],[ 7, 8, 4 ] ]
                    final = [ [ 1, 2, 3 ],[ 5, 8, 6 ],[ 0, 7, 4 ] ]
                    empty_tile_pos = [ 1, 2 ]
                    solve(initial, empty_tile_pos, final)
                    
                    
                    OUTPUT:
                    
                              1  2  3  
                              5  6  0  
                              7  8  4  

                              1  2  3  
                              5  0  6  
                              7  8  4  

                              1  2  3  
                              5  8  6  
                              7  0  4  

                              1  2  3  
                              5  8  6  
                              0  7  4  
---------------------------------------------------------------------------------------------------------------------------------------------------------

   #8-Puzzle Problem
  
                    from sys import maxsize
                    from itertools import permutations
                    V = 4

                    def travellingSalesmanProblem(graph, s):
                        # store all vertex apart from source vertex
                        vertex = []
                        for i in range(V):
                            if i != s:
                                vertex.append(i)

                        # store minimum weight Hamiltonian Cycle
                        min_path = maxsize
                        next_permutation=permutations(vertex)
                        for i in next_permutation:
                           # store current Path weight(cost)
                            current_pathweight = 0

                            # compute current path weight
                            k = s
                            for j in i:
                                current_pathweight += graph[k][j]
                                k = j
                            current_pathweight += graph[k][s]
                             # Update minimum
                            min_path = min(min_path, current_pathweight)
                        return min_path

                    # Driver Code
                    if __name__ == "__main__":

                        # matrix representation of graph
                        graph = [[0, 10, 15, 20], [10, 0, 35, 25],
                                [15, 35, 0, 30], [20, 25, 30, 0]]
                    s = 0
                    print(travellingSalesmanProblem(graph, s))
                    
                    OUTPUT:
                    
                        80
------------------------------------------------------------------------------------------------------------------------------------------------------                        
