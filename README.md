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
