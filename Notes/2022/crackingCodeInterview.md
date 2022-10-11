# Cracking the Coding Interview

1. Interview feedback: Analytical Ability, Coding, Experience, and Communication. 
2. Product Management: Handling Ambiguity, Customer Focus(Attitude, Technical Skills), Multi-level Communication, Passion for Technology, Teamwork.
3. Resume show what you did, how you did, and what the results were. Example:
    - reduced rendering time by 75% by implementing distributed caching, leading to a 10% reduction in log-in time.
    - increased average match accuracy from 1.2 to 1.5 by implementing a new comparision algorithim based on windiff. 
4. Describe skills/languages in plain English, don't list number of years of experience: JavaScript(expert), Python(proficient), Go(prior experience)
5. Interview Preparation, three projects, for each project talk about:
    - Challenges
    - Mistakes/Failures
    - Enjoyed
    - Leadership
    - Conflicts
    - What you'd do differently
6. **Focus on Yourself, Not your team**
7. Tell me about a xxx: Situation -> Action -> Result
8. O(x!) > O(2^x) > O(x^2) > O(xlog x) > O(x) > O(log x)
9. Need to know: 
    - Data Structures: linked lists, tree, tries, graphs, stack, queue, heap, vector/arraylists, hash table
    - Algorithms: Breadth-First Search, Depth-First Search, Binary Search, Merge Sort, Quick Sort
    - Concepts: Bit Manipulation, Memory(Stack vs Heap), Recursion, Dynamic Programming, Big O Time & Space
10. Problem-solving flowchart: Listen -> Example -> Brute Force(state a naive algorithm and **its runtime**)->Optimize(**B**ottlenecks, **U**nnecessary Work, **D**uplicated Work) -> Walk Through your approach in detail -> Implement(keep talking) -> Test(code review, small test cases, edge cases, fix bug)
11. Keep Interviewing at least once a year, even if you aren't actively looking for a new job. This will keep your skill fresh and what opportunities/salaries are out there. 
12. Linked list, fast/slow pointer, 
    - Floyd cycle detection algorithm: fast=slow=head, if fast=slow => there is cycle. Move one pointer start from head, one pointer keep go next, once they meet each other, that's where the cycle start.
14. Tree traversal(always left to right, if root is in the mid, it is in-order, if root is begining, it is pre-order)
    - in-order: left->root->right
    - pre-order: root->left->right
    - post-order: left->right->root
15. Heap: 
    - implement with array, root is smallest/biggest number.
    - insert, insert at the last position, bubble up
    - remove min/max, swap with the last, bubble down.
16. Bit manipulation(Bitwise). JS is [64 floating digit](https://www.avioconsulting.com/blog/overcoming-javascript-numeric-precision-issues)(that's why it losing percesion, 0.1+0.2 != 0.3)
    - When work on bit, JS convert number from 64 float to 32 signed.
    - -1 => 111...111, -2 => 111...110
    - 001 read, 010 write, 100 execute. Give permission read | myPermission, Check permission read & myPermission.
    - XOR, same is false, different it true. 1^1 = 0, 1^0 = 1, 0^0=0
    - NOT/Negation, ~5 => -5(JS will be -6, need to plus one)
    - Arithmetic Shift(<<, >>) 2 >> 1 => 1 (approxmite equal to divide by 2), 2 << 1 => 4 (approxmite equal to double)
    - Logical right shift(>>>), add 0 to the signed bit, shift everything to right. -1 >>> 1 => 2147483647 = 0111...111
17. Sorting and Searching
    - Bucket sort/Radix sort, e.g. sort million people by age. (age 1 - 100 as bucket) O(bucket * n)
    - Bubble sort, start at begining, swap two elements. O(n^2), Memory O(1)
    - Selection sort, scan the array, find smallest one, O(n^2), Memory O(1)
    - Merge sort, O(n log(n))
    - Quick sort, average O(n log(n)), worst O(n^2), Memory O(log(n))
    
page 148
page 398 system design. 
