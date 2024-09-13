## On Problems and Problem Solving

There are two primary levels of analysis when thinking about problems and problem solving procedures:

- The **pre-representational** – How should problems be described as the formal inputs to
problem-solving procedures?
- The **post-representational** – How effective will different problem-solving procedures
be, given a particular problem formalization

- **How does this concept are related with MOSES - knob creation and knob twiddling**

### 1. **Competent Optimization Overview**

- **General Optimization Definition**: In optimization problems, a solution space and a scoring function are specified, with the goal of finding a solution with a high score.
- **Pre- and Post-Representational Improvements**: Improvements in optimization can be made either before representation (e.g., auto-tuning parameters) or after (e.g., modifying the algorithm to avoid local optima).
- **Heuristic Search**: For problems without structured scoring functions, heuristic approaches like random sampling, hill climbing, or simulated annealing are needed due to limited resources for exhaustive search.

### 2. **Exploiting Regularities in Scoring Functions**

- **Assumption of Regularities**: Optimization methods outperform random search only when regularities in the scoring function exist.
- **Decomposition of Problems**: Regularities are often exploited by decomposing a problem into smaller, independent subproblems. Decomposability is key to tractability.

### 3. **Complete Separability and Estimation-of-Distribution Algorithms (EDA)**

- **Complete Separability**: Ideally, problems can be separated into independent parameters, allowing probabilistic methods like Estimation-of-Distribution Algorithms (EDA) to iteratively sample and refine solutions.

### 4. **Using Probabilistic Approaches for Optimization**

- **Application of EDAs**: Probabilistic-statistical methods (e.g., Bayesian models) are used in optimization when interactions between variables are known. This allows for better learning and search processes.

### 5. **Competent Adaptive Optimization Algorithms**

- **Recent Developments**: Recent competent adaptive algorithms like the Bayesian Optimization Algorithm (BOA) and hierarchical BOA (hBOA) dynamically learn problem decomposition and optimize through evolutionary processes.

### 6. **Bayesian Optimization Algorithm (BOA)**

- **Dynamic Problem Decomposition**: BOA uses Bayesian networks to represent relationships between parameters, learning them dynamically during optimization. hBOA further improves this by adding local structure and promoting solution diversity.

### 7. **Effectiveness of BOA and hBOA**

- **Empirical Success**: BOA and hBOA have been effective on various real-world problems (e.g., Ising spin glasses, MaxSAT), even with imperfect problem encoding.

- The key question to consider is how MOSES approaches a problem, which algorithms it uses and why, and how these concepts relate to achieving the desired goal. 

Define the steps involved in solving and optimizing a specific problem using the concepts we've discussed.

### **Flow of Problem Solving:**

1. **Define the Solution Space**: You first define the problem in terms of parameters or knobs. The set of all possible parameter combinations forms the solution space.
2. **Scoring Function**: The scoring function evaluates each candidate solution (each point in the solution space) based on how well it performs the task.
3. **Finding Regularities**: As you explore the solution space, you look for **regularities** in the scoring function—patterns that indicate how the score changes with different parameters. These regularities guide the optimization process.
4. **Optimization Algorithm**: The algorithm uses the scoring function to explore the solution space and find the combination of parameters that gives the best score. The **scoring function** is key because it helps the algorithm evaluate and compare different solutions.

## Representation-Building

- **Definition of Representation**:
    - A representation is a formal system that makes specific entities or types of information explicit, along with how the system operates on that information.
- **Relationship Between Representation-Building and Adaptive Optimization**:
    - There's a close connection between building effective representations and robust adaptive optimization. Competent optimization methods (like BOA and hBOA) can adjust problem decompositions to handle issues with the representation.
- **Problem Decomposition is Crucial**:
    - For complex problems with interacting subcomponents, finding the correct problem decomposition is often equivalent to solving the problem. In ideal scenarios, both the problem decomposition and the solution set converge simultaneously toward the global optimum.
- **Compact and Correct Decompositions**:
    - Successful optimization is contingent on the existence of a **compact** and **correct** problem decomposition in the decomposition space being searched.
- **Challenges in Decomposition**:
    - Difficulty arises when there is no valid decomposition or when a more effective decomposition cannot be formulated as a probabilistic model over the parameters.
- **Two Potential Approaches to Improve Decompositions**:
    - **(1)** Use a more general modeling language to express problem decompositions.
    - **(2)** Introduce additional mechanisms that modify the representation on which the model operates. The text focuses on the second approach, referred to as **representation-building**.
- **Representation-Building**:
    - This process is similar to pre-representational mechanisms typically handled by humans when setting up an optimization problem. The goal is to present the optimization algorithm with key parameters that enable effective problem decomposition.

- important question to ask is that what representation building is, how it is related with problem decomposition that both have in common and how they can contribute to MOSES.

## Why is Program Learning Different?

- **Program Learning Definition**:
    - Program learning involves a **program space (P)**, a **behavior space (B)**, an **execution function** that maps programs to behaviors, and a **scoring function** that evaluates behaviors. The goal is to find a program that, when executed, results in a high score.
- **Key Properties of Program Learning**:
    - **Open-endedness**: Program space (P) has no fixed upper limit on size, and programs can grow.
    - **Over-representation**: Many programs can map to the same behavior.
    - **Compositional hierarchy**: Programs can contain subprograms, forming a hierarchy.
    - **Chaotic Execution**: Small changes in programs can lead to drastically different behaviors.
- **Challenges in Program Learning**:
    - These properties complicate optimization since even if behaviors map well to scores, the complexity of program space and chaotic execution can make it difficult to find optimal solutions as the problem size grows.

### Summery

- **Pre- and Post-Representational Distinction**: It is crucial to differentiate between the stages before (pre-) and after (post-) defining the representation of a problem when thinking about solving it.
- **Role of Competent Evolutionary Optimization Algorithms**: These algorithms are important because they can efficiently solve problems with compact decompositions by following normative principles in the post-representational stage.
- **Challenge of Representation-Building**: One key issue is **representation-building**, where problems need to be framed in a way that allows the optimization algorithm to manipulate (or "twiddle") parameters effectively. The goal is to find an encoding that allows for a **compact problem decomposition**.
- **Program Learning Complexity**: Program learning problems often **lack compact decompositions** due to inherent properties of program spaces and the mapping between programs and behaviors. This makes the problem more complex and harder to decompose.
- **Intractability of Problem Formulations**: Even if the behaviors and scores have a separable structure, the overall complexity of program spaces often leads to intractable problem formulations. In these cases, practitioners often need to manually perform representation-building on a case-by-case basis.
- **Thesis Statement**: The main thesis is that the inherent properties of programs and program spaces can be **used as inductive bias** to reduce the need for manual representation-building, facilitating **competent program evolution**.