def is_safe(vertex, color, graph, colors, num_vertices):
    for neighbor in range(num_vertices):
        if graph[vertex][neighbor] == 1 and colors[neighbor] == color:
            return False
    return True

def graph_coloring_backtracking_util(graph, num_colors, colors, vertex, num_vertices):
    if vertex == num_vertices:
        return True

    for color in range(1, num_colors + 1):
        if is_safe(vertex, color, graph, colors, num_vertices):
            colors[vertex] = color
            if graph_coloring_backtracking_util(graph, num_colors, colors, vertex + 1, num_vertices):
                return True
            colors[vertex] = 0

    return False

def graph_coloring_backtracking(graph, num_colors):
    num_vertices = len(graph)
    colors = [0] * num_vertices

    if not graph_coloring_backtracking_util(graph, num_colors, colors, 0, num_vertices):
        print(f"No solution exists with {num_colors} colors.")
        return None

    return colors

# Example usage:
graph = [
    [0, 1, 1, 1],
    [1, 0, 1, 0],
    [1, 1, 0, 1],
    [1, 0, 1, 0]
]
num_colors = 3

coloring_solution = graph_coloring_backtracking(graph, num_colors)

if coloring_solution:
    print(f"Graph Coloring Solution with {num_colors} colors:")
    for i, color in enumerate(coloring_solution):
        print(f"Vertex {i + 1}: Color {color}")
