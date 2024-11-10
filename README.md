# bees-and-flowers-counter

def bees_between_flowers(s, startIndex, endIndex):
    # Preprocess flower positions and cumulative bee count
    flowers = []
    bee_count = [0] * len(s)
    count = 0
    
    for i, char in enumerate(s):
        if char == '|':
            flowers.append(i)
        elif char == '*':
            count += 1
        bee_count[i] = count
    
    results = []
    for start, end in zip(startIndex, endIndex):
        start -= 1  # Convert 1-indexed to 0-indexed
        end -= 1    # Convert 1-indexed to 0-indexed
        
        # Find the closest flower on or after `start`
        left_flower = next((f for f in flowers if f >= start), None)
        
        # Find the closest flower on or before `end`
        right_flower = next((f for f in reversed(flowers) if f <= end), None)
        
        if left_flower is not None and right_flower is not None and left_flower < right_flower:
            # Bees count between the two flowers
            result = bee_count[right_flower] - bee_count[left_flower]
            results.append(result)
        else:
            results.append(0)
    
    return results

# Sample input for custom testing
s = "|*|*|"
startIndex = [1]
endIndex = [5]

# Running the function
print(bees_between_flowers(s, startIndex, endIndex))  # Expected output: [1]
