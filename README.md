# LEETCODE-Hash_Table-432
Let's walk through a dry run of your `AllOne` class and its operations step by step.

### Class Overview:
- `Node`: Each node represents a count of how many times keys have been incremented. It holds:
  - `count`: the frequency of the keys in that node.
  - `keys`: a set of strings that have this frequency.
  - `prev` and `next`: pointers to previous and next nodes in the doubly linked list.

- `AllOne`: This class keeps track of a doubly linked list of `Node` objects. Each node holds a frequency count, and the linked list helps in efficiently retrieving the max and min keys.

### Scenario:

1. **Initial Setup**:
   - We create an instance of `AllOne()`. This initializes an empty doubly linked list with `head` and `tail` acting as sentinel nodes:
     ```
     head (count = 0) <-> tail (count = 0)
     ```

2. **Inserting a Key**:
   - `inc("apple")`: The key "apple" is new, so it’s added to the `keyToNode` map with an initial frequency of 1.
   - Since `head.next.count != 1`, a new node with `count = 1` is inserted between `head` and `tail`:
     ```
     head (count = 0) <-> (count = 1, keys = { "apple" }) <-> tail (count = 0)
     ```

3. **Incrementing the Same Key**:
   - `inc("apple")`: Now the key "apple" exists, so we increment its frequency.
   - The node with `count = 1` removes "apple" from its keys and inserts it into a new node with `count = 2`. The structure now looks like this:
     ```
     head (count = 0) <-> (count = 2, keys = { "apple" }) <-> tail (count = 0)
     ```

4. **Inserting Another Key**:
   - `inc("banana")`: A new key "banana" is inserted with `count = 1`.
   - Since there's no node with `count = 1`, a new node is inserted between `head` and the node with `count = 2`:
     ```
     head (count = 0) <-> (count = 1, keys = { "banana" }) <-> (count = 2, keys = { "apple" }) <-> tail (count = 0)
     ```

5. **Incrementing "banana"**:
   - `inc("banana")`: The key "banana" is incremented to `count = 2`.
   - "banana" is moved from the node with `count = 1` to the node with `count = 2`, and the node with `count = 1` is removed since it becomes empty:
     ```
     head (count = 0) <-> (count = 2, keys = { "apple", "banana" }) <-> tail (count = 0)
     ```

6. **Decrementing a Key**:
   - `dec("apple")`: The key "apple" is decremented to `count = 1`.
   - A new node with `count = 1` is inserted between `head` and the node with `count = 2`:
     ```
     head (count = 0) <-> (count = 1, keys = { "apple" }) <-> (count = 2, keys = { "banana" }) <-> tail (count = 0)
     ```

7. **Retrieving Max and Min Keys**:
   - `getMaxKey()`: The max key is in the node just before `tail`, which holds `count = 2`. One of the keys in this node is "banana".
   - `getMinKey()`: The min key is in the node just after `head`, which holds `count = 1`. One of the keys in this node is "apple".

### Final Structure:
After these operations, the structure looks like this:
```
head (count = 0) <-> (count = 1, keys = { "apple" }) <-> (count = 2, keys = { "banana" }) <-> tail (count = 0)
```

### Key Points:
- `inc`: Adds or increments keys and adjusts the node placement in the list.
- `dec`: Decrements the key's count and potentially removes the node if it's empty.
- `getMaxKey` and `getMinKey`: Efficiently retrieve the max and min keys by checking nodes adjacent to `tail` and `head`.

This design ensures efficient O(1) operations for all functions.
