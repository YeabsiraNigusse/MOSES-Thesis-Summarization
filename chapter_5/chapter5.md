# Chapter 5

Section 5.1 of the thesis discusses **program-level difficulty**, focusing on how challenging it is to search for an optimal solution within a **deme** (a group of related programs). The core idea is to understand how to choose the **population size (N)** and the **number of generations (G)** to make the search efficient and find the global optimum.

### **Key Focus:**

The section emphasizes the difficulty of program evolution within a **fixed-length representation** (a set of parameters or "knobs") and explores how **N** and **G** impact the ability to find a solution efficiently. The process relies on **competent adaptive optimization algorithms**, such as the **Bayesian Optimization Algorithm (BOA)** or **hierarchical BOA (hBOA)**.

---

### **Key Concepts:**

1. **N (Population Size)**:
    - Refers to the number of programs (or solutions) maintained in a population during the search process.
    - **N** must be large enough to ensure that the initial population contains a wide range of possible sub solutions, to maintain diversity as the search progresses, and to enable effective decision-making in selecting superior sub solutions.
2. **G (Number of Generations)**:
    - Refers to the number of cycles (iterations) that the search algorithm will go through, refining the population with each generation.
    - **G** helps determine how long the search should continue to evolve programs toward an optimal solution.

---

### **Factors Influencing N (Population Size)**

To determine an appropriate population size (N), several factors need to be considered:

1. **Sufficient Initial Diversity**:
    - The population must be large enough to include all necessary **sub solutions** with a high probability. This ensures that the initial population has enough diversity to combine and evolve toward an optimal solution.
    - For example, in a complex problem with k variables, N grows exponentially with k to ensure the right sub solutions are present.
2. **Correct Decision-Making**:
    - During the search, the population size must be large enough to statistically **distinguish** between better and worse sub solutions. This ensures that superior sub solutions are selected and propagated in future generations.
    - For binary problems with n variables, the minimum population size is **O(2^k√n)**, accounting for collateral noise (random variations that can interfere with decision-making).
        
        
3. **Maintaining Diversity**:
    - As the search progresses, diversity must be preserved to avoid **drift**, where important sub solutions are lost. The required **N** depends on the problem's scaling (how different subproblems are weighted in the scoring function).
    - For uniformly scaled problems, N is **O(√n)**, and for exponentially scaled problems, N is **O(n)**.
4. **Learning the Correct Problem Decomposition**:
    - The algorithm must learn the correct **problem decomposition** (how the variables or subproblems interact). A failure to do so increases the population size exponentially, making the search inefficient.
    - In BOA, the population size needed to learn the decomposition is **O(2^k \cdot n^1.05)**. This requirement dominates, and estimating the correct k value (size of sub solutions) becomes crucial.

---

### **Factors Influencing G (Number of Generations)**

The number of generations (G) determines how long the search runs until it converges. Several approaches are discussed for deciding when to stop:

1. **Convergence**:
    - **G** is the number of iterations needed for the population to converge to a single solution, ideally the global optimum.
    - For BOA, the search typically ends when the population converges, but for hBOA (which maintains multiple promising solutions), the population may not fully converge due to **niching**.
2. **Practical Stopping Criteria**:
    - For hBOA, it’s recommended to terminate the search after a number of generations equal to the **number of bits** in the solution encoding, which aligns with convergence theory. In practice, this would be between **O(√n)** and **O(n)** generations.
    - Another guide is to stop the search if no improvements are observed after **O(√n)** generations (the **takeover time**).
3. **Restricted Tournament Replacement (RTR)**:
    - hBOA uses **RTR** to maintain diversity and control when a new solution replaces an existing one in the population. It compares the new solution to a random sample of existing ones, replacing the most similar instance if the new one has a better score.
    - Niches in the population may converge independently, so if no improvements are observed in the last **⌈√(N/w)⌉** generations (where w is the window size in RTR), the search can be terminated.

---

### **Program-Level Difficulty in Summary**

- **Program-level difficulty** depends on:
    1. **n**: The number of problem variables (program size).
    2. **k**: The size of the largest sub solution needed for optimization.
    
    The difficulty arises from the interplay between the program size (n), program evaluation semantics, and the **representation-building** process, which impacts how well the algorithm can explore and optimize different parts of the problem.
    
- The search within a deme involves finding a balance between maintaining enough diversity (N) and determining when to stop the search (G) to efficiently reach the global optimum. The process relies on learning the right decomposition of the problem and ensuring that important sub solutions are not lost along the way.

---

### **Example of Program-Level Difficulty in MOSES**:

Imagine you are trying to optimize a program with 10 binary variables. The population size **N** must be large enough to cover all possible sub solutions. Let’s say **N** is set to 200 to ensure sufficient diversity in the initial population. The number of generations **G** would determine how many iterations the algorithm will take to recombine, mutate, and optimize these programs.

During the search:

- **N** ensures the population contains enough variation to explore the problem space efficiently.
- **G** ensures the search runs long enough to find the optimal solution, stopping when no further improvements are observed.

In the end, the program-level difficulty is about balancing these two parameters to solve the problem efficiently while avoiding unnecessary computation or getting stuck in suboptimal solutions.

## 5.2 Deme-Level Difficulty

In section 5.2, titled "Deme-Level Difficulty," the thesis addresses the complexity encountered at the deme level of the MOSES algorithm, which is concerned with decomposing and optimizing solutions within subspaces of programs (demes). A "deme" represents a population of related programs, and the primary goal is to evolve solutions within these subspaces to find local or global optima.

Key points include:

1. **Deme-Level Optima**: Each deme contains a program that is optimal within its region. This is called a "deme-local optimum." However, this is different from a local optimum, as the latter refers to neighboring programs, while deme regions are exponentially larger than local neighborhoods. This helps in focusing on broader search areas.
2. **Deme Reachability**: The concept of "strict deme-reachability" indicates that some global optima can be reached from the initial program through a series of intermediate deme-local optima. If all global optima can be reached this way, the problem is deemed "deme-separable." MOSES is designed to proceed to a global optimum by solving smaller sub-problems within each deme.
3. **Neutrality**: The discussion highlights the challenge of neutrality, where many solutions in a deme may have the same or very similar scores. This makes it difficult to identify a clear path to global optima, as many programs might be functionally equivalent, and MOSES must navigate this large network of near-optimal programs.
4. **Deme Management**: The algorithm uses heuristics to manage the creation and elimination of demes, selecting exemplars (leading programs) that are not behaviorally dominated by others in the deme. New demes are created when promising programs are found, and demes with the highest-scoring exemplars are favored for further optimization.
5. **Challenges**: One of the challenges MOSES faces is that in practice, strict deme-reachability might not hold. Neutrality and redundancy can complicate the path to the global optimum, resulting in numerous near-equivalent solutions. Consequently, the process may involve wading through a vast number of demes before finding a global solution, adding to computational difficulty.

In summary, **deme-level difficulty** in MOSES is influenced by the management of program space subdivisions, the presence of neutrality, and the need for smart strategies to find global solutions while navigating the numerous near-optimal local solutions within each deme.

[Detail view](https://www.notion.so/Detail-view-ac142f5203d64f53aa27679e44ee4e82?pvs=21)