a Radix Tree is a type of tree that compresses non-branching paths
so it drops the ram usage and number of lookups that need to be made.

normal standard trie:

```
								 (root)
								         |
								        '/'
								         |
								        'a'
								         |
								        'p'
								         |
								        'i'
								         |
								        '/'
								         |
								        'v'
								       /   \
								     '1'   '2'  <-- [/api/v2]
								      |
								     '/'
								     / \
								   'u' 'p'
								
								   |   |
								  's' 'o'
								
								   |   |
								  'e' 's'
								
								   |   |
								  'r' 't'
								
								   |   |
								  's' 's'       <-- [/api/v1/posts]
								   |
								[/api/v1/users]
```

Radix Tree:
```
         (root)
           |
       "/api/v"
        /    \
      "1"    "2"  <-- [/api/v2]
       |
      "/"
     /   \
"users" "posts"

   |       |
   |   [/api/v1/posts]
   |
[/api/v1/users]

```



- **k**: Length of the longest key.
- **n**: Total number of keys stored in the tree.
- **r**: The radix or alphabet size (e.g., `r = 2` for binary, `r = 26` for lowercase English letters).

| Operation            | Average Case | Worst Case |
| -------------------- | -----------: | ---------: |
| Search               |       `O(k)` |     `O(k)` |
| Insertion            |       `O(k)` |     `O(k)` |
| Deletion             |       `O(k)` |     `O(k)` |
| **Space Complexity** |   `O(n · k)` | `O(n · k)` |