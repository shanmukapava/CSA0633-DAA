INF = float('inf')

def floyd_algorithm(graph):
    n = len(graph)
    
    # Initialize the distance matrix
    dist = [[INF] * n for _ in range(n)]
    for i in range(n):
        dist[i][i] = 0
        for j, weight in enumerate(graph[i]):
            if weight != 0:
                dist[i][j] = weight
    
    # Update the distance matrix using Floyd's Algorithm
    for k in range(n):
        for i in range(n):
            for j in range(n):
                if dist[i][k] != INF and dist[k][j] != INF and dist[i][k] + dist[k][j] < dist[i][j]:
                    dist[i][j] = dist[i][k] + dist[k][j]

    return dist

# Example usage:
graph = [
    [0, 3, 0, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 0, 7, 0],
    [2, 0, 0, 0, 1],
    [0, 0, 0, 0, 0]
]

result = floyd_algorithm(graph)

print("Shortest distances between all pairs:")
for row in result:
    print(row)
