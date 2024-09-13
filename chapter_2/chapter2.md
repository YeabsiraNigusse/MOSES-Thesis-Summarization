why do we care about representation building

- Reduces Search Space Complexity
- it helps for problem decomposability
- Improves Adaptability - faster way to get regularities
- Facilitates Competent Search - effective way of solution finding

[Detail View](https://www.notion.so/Detail-View-8416013bbc164ac18c6b2b22f0343ece?pvs=21)

[Examplar](https://www.notion.so/Examplar-70935d80d28d4630a29748493f25f480?pvs=21)

### MOSES Overview:

- MOSES uses **competent optimization algorithms** to create new solutions by dynamically learning and decomposing problems. This approach is unique in handling the complexities of **program learning**.
- The chapter emphasizes that MOSES effectively decomposes problems through dynamic representation building, optimizing the search process by focusing on promising subspaces.

### Section 2.1: Statics (Representation Building)

- **Representation Building**: The goal is to exploit regularities in program spaces, especially **behavioral decomposability** and **white box execution**, to dynamically construct representations that **limit and transform** the search space into a **compact, relevant subspace**.
- Example (Figure 2.1): Three program trees (with identical structures) are presented, encoding real-valued expressions. The corresponding behavioral patterns (Figure 2.2) demonstrate how these programs behave across variable inputs. This visual comparison helps **decompose** the problem based on behavior rather than syntactic variations.

### Variations on a Theme (Section 2.1.1):

- **Knobs** (parameters that control program behavior) are introduced. These knobs should represent distinct and meaningful changes in behavior, not just in program syntax.
    - Example: Different ways to modify cosine expressions, weighted averages of inputs, or adjusting the weight of components in the program.

### Summary of Section 2.1.2: Syntax and Semantics

This section discusses the challenges and principles of **representation-building** in program evolution by aligning **syntactic and semantic variations**. Several issues, such as **over-representation** and **chaotic execution**, complicate this process:

1. **Non-Orthogonality**:
    - Caused by **over-representation**: For example, commutative and associative properties allow many syntactic variations of the same operation, such as a1+a2+...+an represented in many ways.
        
        a1+a2+...+ana_1 + a_2 + ... + a_n
        
    - Similar redundancy exists in **Boolean formulas**, **list manipulations**, and **conditionals**. Eliminating these redundancies fully is infeasible, but heuristic approaches can partially address them.
2. **Oversampling of Distant Behaviors**:
    - Due to chaotic execution and over-representation, **simpler programs** are often oversampled, resulting in redundant evaluations.
    - Simplicity here is defined by the **minimal length** of a program that achieves a specific behavior.
3. **Under sampling of Nearby Behaviors**:
    - Syntactically diverse programs may exhibit similar behaviors, leading to **under sampling** of semantically close programs.
    - Example: 3×x versus x+x+x demonstrates syntactically different expressions but with the same behavior.
        
        3×x3 \times x
        
        x+x+xx + x + x
        
    - These organizational principles guide how program search spaces are explored.

### Organizational Principles:

- **Differing organizational principles** bias the sampling of nearby behaviors. For instance, programs organized differently might have identical performance scores but represent different paths toward solving a problem.
- MOSES seeks to address **under sampling** by managing **neutrality in search**, exploring how variations impact program behaviors without being overwhelmed by irrelevant syntactic differences.

[Detail view](https://www.notion.so/Detail-view-accef2bf24d74c13bb79712c19279918?pvs=21)

the process MOSES uses to build a set of parameters or "knobs" for generating and optimizing programs. It involves three key steps:

1. **Reduction to Normal Form**: Redundant parts of the program are removed using heuristic rules (e.g., simplifying expressions like "x + 0 → x"). This ensures that the program is in its simplest form without unnecessary complexity.
2. **Neighborhood Enumeration**: Once the program is simplified, a set of possible variations (perturbations) is generated. These variations are intended to explore small, behaviorally similar changes to the original program.
3. **Neighborhood Reduction**: Redundant or overly complex variations are eliminated to focus on meaningful changes. This is done by checking if applying a variation results in a significant simplification, which could indicate redundancy.

### Section 2.2: Dynamics

This section of the dissertation discusses the **dynamics of MOSES (Meta-Optimizing Semantic Evolutionary Search)** in constructing and managing program spaces. MOSES operates by dynamically creating a parameterized representation of a certain region in program space, focusing on one or more exemplar programs. The main goal is to develop a compact problem decomposition through representation-building.

- **Representation Building**: MOSES creates a parameterized representation around an exemplar program, or closely related programs, to create meaningful variations.
- **Deme Concept**: A sample of programs within a representation is called a "deme," and a collection of demes forms a "metapopulation." MOSES evolves these demes by adaptively allocating computational resources based on their promise in solving the problem.
- **Deme Management**: MOSES integrates deme management by adaptively creating new demes, discarding less effective ones, and allocating more computational effort to more promising demes. This is important for navigating the large search space of possible programs.
- **Algorithm Sketch**:
    1. **Initial Program Sampling**: It begins by generating an initial random sampling of programs.
    2. **Modeling Promising Programs**: From the existing sample of programs, promising ones are chosen for further exploration, based on a scoring function.
    3. **Optimization Process**: The system applies optimization algorithms to tweak the programs and create new variations.

The main architectural components of MOSES include the representation-building process, random sampling, scoring, and optimization, with only the scoring function being problem-specific.