# Algorithms: Study Notes with Explanations

*Fundamentals of algorithms, correctness, NP-completeness and efficiency, based on handwritten class notes*

## 1. What Is an Algorithm?

**From the notes:** An algorithm is a well-defined computational procedure that takes a value or a set of values as input and gives a value or a set of values as output in a finite time. It describes an input → output relationship, and it is a tool for solving a computational problem.

**Explanation:** Think of an algorithm as a precise recipe. Three ideas matter in the definition. *Well-defined* means every step is exact, with no guessing. *Input and output* means it transforms something given into something wanted. *Finite time* means it must eventually stop. A **problem** states the relationship we want (for example, arrange these numbers in order), and the **algorithm** is the method that produces it. One problem can have many algorithms, such as insertion sort and merge sort for sorting.

## 2. Example: The Sorting Problem

**From the notes:**

- **Input:** a sequence of numbers (a₁, a₂, a₃, …, aₙ).
- **Output:** a permutation (a₁′, a₂′, a₃′, …, aₙ′) such that a₁′ ≤ a₂′ ≤ a₃′ ≤ … ≤ aₙ′.
- The input that is given is called an **instance of the problem**. An instance "promises" to respect the constraints imposed by the problem.

**Explanation:** A *permutation* is the same set of numbers rearranged, so nothing is lost or added. The *problem* is general (sort any list), while an *instance* is one concrete case, such as (5, 2, 9, 1), whose answer is (1, 2, 5, 9). The *promise* is the problem's assumptions about valid input. For sorting, the items must be numbers that can be compared with ≤. An algorithm only has to work for valid instances, but it must work for **every** one of them.

## 3. When Is an Algorithm Correct?

**From the notes:** An algorithm is correct if it halts in finite time and does not give wrong answers. An algorithm is incorrect for two reasons: (1) it does not halt, or (2) it halts but gives a wrong answer.

**Explanation:** Correctness has two parts: *termination* and *right output*. A loop whose counter is never updated breaks the first rule because it runs forever. A routine that returns the first element as "the smallest" without checking the rest breaks the second rule because it stops quickly with the wrong result. A correct algorithm gives the right output for every valid instance, not just for the examples you tried.

*Transcription note: the notes read "cannot give correct answers" at this point. I have read this as "cannot give incorrect answers", which matches the standard definition. Please check it against your class material.*

## 4. How Can an Algorithm Be Expressed?

**From the notes:** An algorithm can be written in English or another language, as a computer program, or as a hardware design. The only requirement is a precise description of the procedural computation.

**Explanation:** The form is flexible, but precision is not. A paragraph of plain English, pseudocode, Java code and a digital circuit can all describe the same algorithm, as long as each step is unambiguous and can be carried out mechanically. This is why textbooks use pseudocode. It is exact without being tied to one programming language.

## 5. Incorrect Algorithms Can Still Be Useful

**From the notes:** Incorrect algorithms are useful when the error rate can be controlled.

**Explanation:** Sometimes a perfect answer costs too much time, and an answer that is almost always right is good enough. A well-known example is the Miller–Rabin primality test, which is a randomized algorithm. It can be wrong with a tiny probability, and repeating it makes that probability negligible, so it is used in real cryptography software. The key condition in your note is *controlled*. We need to know how often it errs and be able to reduce it.

## 6. Data Structures

**From the notes:** A data structure is a way to store and organize data in order to facilitate access and modification.

**Explanation:** How data is arranged decides how fast operations are. Common examples are arrays, linked lists, stacks, queues, hash tables, trees and graphs. Searching a sorted array with binary search is far faster than scanning an unsorted one item by item. No single structure is best for everything, so choosing one involves trade-offs, and algorithms and data structures are almost always studied together.

## 7. NP-Complete Problems

**From the notes:**

- NP-complete problems are problems for which no efficient algorithm is known.
- Nobody has ever proved that an efficient algorithm for one of them cannot exist.
- If an efficient algorithm exists for any one of them, then one exists for all of them.
- Several NP-complete problems are similar but not identical. A small change in the problem statement can cause a big change in the efficiency of the best known algorithm.

**Explanation:** "Efficient" here means polynomial time, such as n or n², rather than exponential time, such as 2ⁿ. These problems are all linked, so a fast solution to one would give a fast solution to all of them. That is the heart of the famous **P vs NP** question, which is still open. A classic example of the "small change" idea: finding a route that crosses every **edge** of a graph exactly once (an Euler tour) has a fast algorithm. Changing the wording to visit every **vertex** exactly once (a Hamiltonian cycle) makes it NP-complete. In practice, once you recognize a problem as NP-complete, you stop searching for a perfect fast algorithm and use approximations or heuristics instead.

## 8. Online Algorithms

**From the notes:** An online algorithm is one in which the input arrives over time rather than being available all at the start.

**Explanation:** The algorithm must make decisions without knowing what will come next. Examples include deciding which page to evict from a cache, handling requests as they arrive at a server, and processing live data streams. This contrasts with ordinary "offline" problems such as sorting, where the whole list is given up front.

## 9. Why Efficiency Matters: Resources Are Limited

**From the notes:** Computers will not run infinitely fast, and they have neither infinite nor free memory. Therefore algorithms must use the resources of time and space efficiently.

**Explanation:** Every algorithm consumes two resources. **Time** is how many steps it takes, and **space** is how much memory it needs. Because both are limited and cost something, we compare algorithms by how these requirements grow as the input gets larger. Sometimes we trade one for the other by spending extra memory to save time, or the reverse.

## 10. Measuring Efficiency: Insertion Sort vs Merge Sort

**From the notes:** Two computers sort the same large list with different algorithms.

- **Computer A (faster computer):** runs insertion sort at 10⁹ instructions per second. Time complexity is c₁n² with c₁ = 2.
- **Computer B (slowest computer):** runs merge sort at 10⁷ instructions per second. Time complexity is c₂ n lg n with c₂ = 50.
- Both sort n = 10⁷ numbers. The constants c₁ and c₂ do not make much difference, and c₁ < c₂.

**Computer A (insertion sort):**

Time = c₁n² ÷ instructions per second = 2 × (10⁷)² ÷ 10⁹ = 2 × 10¹⁴ ÷ 10⁹ = **2 × 10⁵ seconds**, which is about 55.6 hours.

**Computer B (merge sort):**

Time = c₂ n lg n ÷ instructions per second = 50 × 10⁷ × lg(10⁷) ÷ 10⁷ = 50 × lg(10⁷) = 50 × 23.25 ≈ **1,163 seconds**, which is about 19.4 minutes.

**Explanation:** Insertion sort has the smaller constant (2 against 50), and it runs on hardware 100 times faster. It still loses badly. The reason is the growth rate. Insertion sort grows like n², so doubling the input roughly quadruples the work. Merge sort grows like n lg n, and lg 10⁷ is only about 23, so each number costs just 23 "steps" of work. At n = 10⁷, merge sort on the slow machine finishes about **172 times sooner**. For small inputs the constants can matter, but as n grows the better growth rate always wins.

## 11. Key Takeaway

**From the notes:** Even with a supercomputer, insertion sort can be beaten by merge sort running on a slower computer.

**Explanation:** Faster hardware gives a constant-factor speedup, but a better algorithm changes the growth rate, and that gap widens as the input grows. This is why algorithm design and analysis matter as much as hardware. An efficient algorithm is a technology in its own right.
