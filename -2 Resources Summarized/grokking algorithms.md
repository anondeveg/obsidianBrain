---
tags:
  - Resources_Summarized
---

2026-02-22 03:13

**Source material** : Grokking Algorithms
**Tags** : [[algorithms]], [[graphs]], [[BFS]], [[dijkstra]], [[recursion]], [[big-o]], [[greedy]]

# Grokking Algorithms — Vault Notes

### BFS vs Dijkstra: Shortest Path Criteria

* **BFS (Breadth-First Search):** Finds the shortest path by the fewest edges in an unweighted graph. If all edges have equal weight, this also corresponds to the shortest-time path.
* **Dijkstra's Algorithm:** Finds the shortest path by minimum total weight (time/cost) in a weighted graph with non-negative weights. It minimizes the total weight along the path, not the number of edges.

### Dijkstra’s Four-Step Intuition

1. **Pick:** Select the unvisited node with the smallest distance from the source.
2. **Mark:** Mark it as visited (this is your current node).
3. **Update:** For each neighbor of the current node, update its distance if a shorter path through the current node is found.
4. **Repeat:** Continue until all nodes are visited or the target is reached.

* **Final path calculation:** After finishing, backtrack from the target via predecessors to reconstruct the actual path. You can stop early if the target node is popped from the priority queue.

### Graph Types and Correctness

* **Undirected Graphs:** Dijkstra can operate on undirected graphs with non-negative weights. Note that each edge in an undirected graph is bidirectional and can contribute to cycles; the algorithm handles this correctly if weights are non-negative.
* **Directed Acyclic Graphs (DAGs):**  Dijkstra is not restricted to DAGs. DAGs are just a special case where other techniques (like Dynamic Programming on topological order) can solve shortest paths even more efficiently.

---

### Big-O & Sorting Design

* **Sorting:** Because sorting is computationally expensive and takes time to process, a good design always seeks to sort data on input if possible.
* **Constants in Big-O:** In Big-O notation (e.g., ), there is a constant factor () that we usually ignore because it doesn't scale. However, in some real-world performance cases, it *does* matter. Take care of it.
* **Linked Note:** [[BIG-O]] -> `/home/anondev/vaults/brain/BIG-O.md`

---

### Greedy Algorithms

* **Takeaway:** Sometimes, perfect is the enemy of good. Often, all you need is an algorithm that solves the problem "pretty well."
* **Why use them:** Greedy algorithms shine here because they’re simple to write, fast, and usually get pretty close to the optimal solution.

---

### Recursion

* **When to Use It:** Recursion is best used when it makes the solution clearer for the programmer.
* **Performance:** There is generally no performance benefit to using recursion over iteration; in fact, loops are often better for raw performance.
> “Loops may achieve a performance gain for your program. Recursion may achieve a performance gain for your programmer. Choose which is more important in your situation!” — Leigh Caldwell



#### Structure of a Recursive Function

Every recursive function has two parts:

1. **Base Case:** The condition where the function does **not** call itself, preventing infinite recursion.
2. **Recursive Case:** The condition where the function calls itself, continuing the process toward the base case.

---
## Dynamic Programming
Dynamic programming only works when each subproblem is discrete—when it doesn’t depend on other subproblems.

Dynamic programming is useful when you’re trying to optimize
something given a constraint. In the knapsack problem, you had to
maximize the value of the goods you stole, constrained by the size of
the knapsack.

The values in the cells are usually what you’re trying to optimize.
For the knapsack problem, the values were the value of the goods.

Each cell is a subproblem, so think about how you can divide
your problem into subproblems. That will help you figure out what
the axes are.

Every dynamic-programming solution involves a grid.

---

### To Research / Backlog

* **Bellman-Ford algorithm:** Shortest path algorithm capable of handling negative weights (out of scope for *Grokking Algorithms*, but useful for research).
* **Tail recursion:** [[Tail Recursion — Fibonacci Example]]

---
### Fun

But that still doesn’t tell you the formula to use. Computer scientists
sometimes joke about using the Feynman algorithm. The Feynman
algorithm is named after the famous physicist Richard Feynman, and
it works like this:
1. Write down the problem.
2. Think real hard.
3. Write down the solution.


--- 
Thoughts/Philosophy

The truth is, there’s no easy way to calculate the formula here. You
have to experiment and try to find something that works. Sometimes
algorithms aren’t an exact recipe. They’re a framework that you build
your idea on top of.

---
## **References**:

* Grokking Algorithms (including p. 59)
* Leigh Caldwell on Recursion vs. Iteration: [https://stackoverflow.com/questions/72209/recursion-or-iteration/72694#72694](https://stackoverflow.com/questions/72209/recursion-or-iteration/72694#72694)
* Vault Linked Note: `/home/anondev/vaults/brain/BIG-O.md`

---
Parallel algorithms
The next three topics are about scalability and working with a lot of
data. Back in the day, computers kept getting faster and faster. If you
wanted to make your algorithm faster, you could wait a few months,
and the computers themselves would become faster. But we’re near the
end of that period. Instead, laptops and computers ship with multiple
cores. To make your algorithms faster, you need to change them to run
in parallel across all the cores at once!
Here’s a simple example. The best you can do with a sorting algorithm is
roughly O(n log n). It’s well known that you can’t sort an array in O(n)
time—unless you use a parallel algorithm! There’s a parallel version of
quicksort that will sort an array in O(n) time.
Parallel algorithms are hard to design. And it’s also hard to make sure
they work correctly and to figure out what type of speed boost you’ll
see. One thing is for sure—the time gains aren’t linear. So if you have
two cores in your laptop instead of one, that almost never means your
algorithm will magically run twice as fast. There are a couple of reasons
for this:
• Overhead of managing the parallelism—Suppose you have to sort
an array of 1,000 items. How do you divide this task among the two
cores? Do you give each core 500 items to sort and then merge the
two sorted arrays into one big sorted array? Merging the two arrays
takes time.
• Load balancing—Suppose you have 10 tasks to do, so you give each
core 5 tasks. But core A gets all the easy tasks, so it’s done in 10
seconds, whereas core B gets all the hard tasks, so it takes a minute.
That means core A was sitting idle for 50 seconds while core B was
doing all the work! How do you distribute the work evenly so both
cores are working equally hard?

Bloom filters
Bloom filters offer a solution. Bloom filters are probabilistic data
structures. They give you an answer that could be wrong but is probably
correct. Instead of a hash, you can ask your bloom filter if you’ve
crawled this URL before. A hash table would give you an accurate
answer. A bloom filter will give you an answer that’s probably correct:
• False positives are possible. Google might say, “You’ve already crawled
this site,” even though you haven’t.
• False negatives aren’t possible. If the bloom filter says, “You haven’t
crawled this site,” then you definitely haven’t crawled this sit