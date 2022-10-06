import sys
sys.setrecursionlimit(3000)

num_v = int(input()) #Num of vertices

matrix = []
for row in range(num_v):
    matrix.append(list(map(int, input().split()))) #Making a matrix of all connections 

cycle = False
used_v = []
parent = dict()
for i in range(num_v):
    parent[i] = -1
    used_v.append(0)

def dfs (first_vertex):
    global cycle
    global kid
    used_v[first_vertex] = 1
    for vertex in range(num_v): #Searching of a new connected vertex
        if matrix[first_vertex][vertex] == 1 and used_v[vertex] == 0: 
            parent[vertex] = first_vertex
            dfs(vertex)
        elif matrix[first_vertex][vertex] == 1 and used_v[vertex] == 1 and parent[first_vertex] != vertex and not cycle:
            cycle = True 
            parent[vertex] = first_vertex
            kid = first_vertex

for v in range(num_v):
    dfs(v)
    if cycle:
        cycle_path = []
        while kid + 1 not in cycle_path:
            cycle_path.insert(0, kid + 1)
            kid = parent[kid]
        break
    for i in range(num_v):
        parent[i] = -1
        used_v[i] = 0
    
if cycle:
    print('YES')
    print (len(cycle_path))
    print (*cycle_path, sep = ' ')
else:
    print('NO')
