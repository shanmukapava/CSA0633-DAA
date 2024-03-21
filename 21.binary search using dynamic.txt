def optimal_bst(keys, freq):
    n = len(keys)
    
    # Initialize the cost and root tables
    cost = [[0] * n for _ in range(n)]
    root = [[0] * n for _ in range(n)]

    # Initialize the cost table for one-node subtrees
    for i in range(n):
        cost[i][i] = freq[i]
        root[i][i] = i

    # Calculate the cost for all subtrees of increasing lengths
    for length in range(2, n + 1):
        for i in range(n - length + 1):
            j = i + length - 1
            cost[i][j] = float('inf')

            # Try making each key the root and find the optimal cost
            for r in range(i, j + 1):
                c = cost[i][r - 1] + sum(freq[i:r]) + cost[r + 1][j] + sum(freq[r + 1:j + 1])
                if c < cost[i][j]:
                    cost[i][j] = c
                    root[i][j] = r

    return cost, root

def construct_optimal_bst(keys, root, i, j):
    if i > j:
        return None
    root_key = keys[root[i][j]]
    left_subtree = construct_optimal_bst(keys, root, i, root[i][j] - 1)
    right_subtree = construct_optimal_bst(keys, root, root[i][j] + 1, j)
    return {"key": root_key, "left": left_subtree, "right": right_subtree}

# Example usage:
keys = [10, 12, 20]
freq = [34, 8, 50]

cost_table, root_table = optimal_bst(keys, freq)
optimal_bst_structure = construct_optimal_bst(keys, root_table, 0, len(keys) - 1)

print("Optimal BST Cost Table:")
for row in cost_table:
    print(row)

print("\nOptimal BST Root Table:")
for row in root_table:
    print(row)

print("\nOptimal BST Structure:")
print(optimal_bst_structure)
