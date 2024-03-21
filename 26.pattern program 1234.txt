def print_pattern(n):
    for i in range(1, n + 1):
        # Print spaces
        for j in range(n - i):
            print(" ", end=" ")

        # Print numbers
        for k in range(1, i + 1):
            print(k, end=" ")

        # Move to the next line after each row
        print()

# Example usage:
n = 4
print_pattern(n)
