
# Huffman Coding

## Aim

To implement Huffman coding to compress the data using Python.

## Software Required

1. Anaconda - Python 3.7
2. Jupyter Notebook / VS Code
3. Python Libraries: heapq, collections

## Algorithm

**Step 1:**

Get the input string from the user.

**Step 2:**

Calculate the frequency of occurrence of each character in the input string using Counter.

**Step 3:**

Create tree nodes for each character and insert them into a priority queue based on their frequency.

**Step 4:**

Construct the Huffman tree by repeatedly removing the two nodes with the lowest frequencies and combining them into a new node until only one node remains.

**Step 5:**

Traverse the Huffman tree to generate binary codes. Assign 0 to the left branch and 1 to the right branch. Print each character, its frequency, and its Huffman code.

## Program

```python
import heapq
from collections import Counter

# Create tree nodes
class Node:
    def __init__(self, char, freq):
        self.char = char
        self.freq = freq
        self.left = None
        self.right = None

    def __lt__(self, other):
        return self.freq < other.freq


# Generate Huffman codes
def generate_codes(root, current_code, codes):
    if root is None:
        return

    if root.char is not None:
        codes[root.char] = current_code if current_code else "0"
        return

    generate_codes(root.left, current_code + "0", codes)
    generate_codes(root.right, current_code + "1", codes)


# Main function to implement Huffman coding
def huffman_coding(text):
    if not text:
        print("Input string is empty.")
        return

    # Calculate frequency of occurrence
    frequency = Counter(text)

    # Create priority queue
    heap = []

    for char, freq in frequency.items():
        heapq.heappush(heap, Node(char, freq))

    # Build Huffman tree
    while len(heap) > 1:
        left = heapq.heappop(heap)
        right = heapq.heappop(heap)

        merged = Node(None, left.freq + right.freq)
        merged.left = left
        merged.right = right

        heapq.heappush(heap, merged)

    # Generate Huffman codes
    codes = {}
    generate_codes(heap[0], "", codes)

    # Print characters and Huffman codes
    print("\nCharacter Frequency Huffman Code")
    print("---------------------------------")

    for char, freq in frequency.items():
        display_char = "SPACE" if char == " " else char
        print(display_char, "      ", freq, "       ", codes[char])

    # Encode the input string
    encoded_text = ""

    for char in text:
        encoded_text += codes[char]

    print("\nOriginal String:", text)
    print("Encoded String:", encoded_text)
    print("Original Size:", len(text) * 8, "bits")
    print("Compressed Size:", len(encoded_text), "bits")


# Get the input string
text = input("Enter a string: ")

# Call Huffman coding function
huffman_coding(text)
```

## Developed By

**Name:** Varun A

**Register No:** 212224240178

## Output

<img width="972" height="352" alt="image" src="https://github.com/user-attachments/assets/ba4f239f-2c46-416b-a1b6-ab588e595735" />



## Result

Thus, the Huffman coding was implemented to compress the data using Python programming.
