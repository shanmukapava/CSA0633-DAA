import itertools

def tsp_dynamic_programming(distances):
    n = len(distances)
    
    # memoization table to store subproblem solutions
    memo = {}
    
    # Helper function to calculate the minimum cost for a specific state
    def tsp_min_cost(mask, current_city):
        if mask == (1 << n) - 1:
            # All cities have been visited, return the cost to return to the starting city
            return distances[current_city][0]
        
        # Check if the subproblem solution is already calculated
        if (mask, current_city) in memo:
            return memo[(mask, current_city)]
        
        # Calculate the minimum cost for the current state
        min_cost = float('inf')
        for next_city in range(n):
            if (mask >> next_city) & 1 == 0:  # Check if the city has not been visited
                new_mask = mask | (1 << next_city)
                cost = distances[current_city][next_city] + tsp_min_cost(new_mask, next_city)
                min_cost = min(min_cost, cost)
        
        # Memoize the solution for this subproblem
        memo[(mask, current_city)] = min_cost
        return min_cost
    
    # Start the dynamic programming process
    initial_mask = 1  # The starting city is always visited first
    min_cost = tsp_min_cost(initial_mask, 0)
    
    return min_cost

# Example usage:
cities_distances = [
    [0, 10, 15, 20],
    [10, 0, 35, 25],
    [15, 35, 0, 30],
    [20, 25, 30, 0]
]

shortest_route_cost = tsp_dynamic_programming(cities_distances)
print(f"The minimum cost of the TSP is: {shortest_route_cost}")
