# Inside G iterations

### **High-Level Overview of the MOSES Process:**

1. **Representation Building**: MOSES begins by creating a **parameterized representation** (a set of "knobs") around an exemplar. The exemplar is the central solution from which variations are explored.
2. **Population (Deme) Initialization**: A population (deme) of size **N** is created based on the representation, consisting of different programs (variations of the exemplar).
3. **Optimization (G Iterations)**: MOSES runs an optimization process over **G** generations, refining the population within each generation.

---

### **What Happens in Each Iteration (G) in MOSES?**

For each iteration GGG, MOSES follows a structured process of **selecting**, **optimizing**, and **evaluating** the programs within the population. Here's a detailed, step-by-step breakdown of what MOSES does:

---

### **Step-by-Step MOSES Algorithm:**

1. **Initialize Population**:
    - The process starts by creating an initial population of **N programs** (the deme) based on the **exemplar** and its associated **representation** (knobs). This population represents different variations of the exemplar.
2. **Select Promising Programs (Selection)**:
    - From the population, MOSES selects **promising programs** (based on the scoring function) to act as models for further optimization.
    - The selection is done by evaluating the **fitness** (quality or score) of each program in the population. Higher-scoring programs are selected as "parents" for the next generation.
    - If there are **ties** in scores between programs, the algorithm favors **smaller programs** (i.e., those with simpler structures or shorter length) to reduce complexity.
3. **Modeling Subsolutions (Optimization)**:
    - Using the selected promising programs, MOSES applies a **competent optimization algorithm** (such as the **Bayesian Optimization Algorithm (BOA)** or **hierarchical BOA (hBOA)**).
    - The optimization algorithm **recombines** the subsolutions (pieces of the program) to create new variations.
    - In other words, **recombination** occurs based on the **knobs** that define the program space. The goal is to find better combinations of subsolutions that improve the overall program's behavior.
4. **Generate New Programs (New Candidates)**:
    - After recombining subsolutions, the algorithm **generates new programs** (new knob settings) from these recombinations.
    - The new programs are evaluated by the **scoring function**, which measures their fitness (how well they perform the task).
    - Each new program is integrated into the population by **replacing less promising programs** (those with lower scores).
5. **Evaluate and Update the Population (Replacement)**:
    - After generating new programs, MOSES **re-evaluates** the entire population to decide which programs will survive into the next generation.
    - The population is **updated** by replacing the weakest programs with the newly generated, higher-scoring programs.
    - This keeps the population **focused** on the most promising solutions, improving the overall quality of the deme with each iteration.
6. **Repeat for G Iterations**:
    - This process of **selection**, **optimization**, **generation**, and **replacement** continues for **G generations**.
    - After each generation, the population improves, gradually converging toward the **global optimum** or the best solution for the problem.
7. **Deme Termination (Stopping Criteria)**:
    - The algorithm can stop once a **convergence criterion** is met (i.e., when the population has stopped improving, or no better programs are being found).
    - For BOA, this could mean waiting until the population converges on a single solution. For hBOA (which maintains multiple promising solutions simultaneously), the algorithm might never fully converge, so the search may be stopped after a certain number of **generations without improvement** or based on **niches** in the population.
    - If the deme produces **new exemplars** (i.e., programs that are non-dominated by the current exemplars), new demes might be created to explore different areas of the solution space.

---

### **Algorithmic Detail of G Iterations in MOSES:**

1. **Population Initialization**: Generate a population (deme) of size **N** around the exemplar using the representation (knobs).
2. **While not converged (run for G generations):**
    - **Select promising programs** from the population based on their fitness scores.
    - **Optimize** by recombining subsolutions of the selected programs (using BOA or hBOA).
    - **Generate new programs** based on recombined subsolutions.
    - **Evaluate** the fitness of the new programs using a scoring function.
    - **Update the population** by replacing low-performing programs with new high-performing programs.
    - **Check for convergence** or stop criteria (e.g., no improvement in recent generations).
3. **End of Generation G**: After G iterations, the best program in the deme is returned, and the algorithm may create new demes based on promising new exemplars.

---

### **Example of G Iterations in MOSES:**

Imagine you are evolving a program to solve a **mathematical optimization** problem. The exemplar program might be a simple mathematical expression like f(x,y)=x2+y2f(x, y) = x^2 + y^2f(x,y)=x2+y2. The knobs represent parameters (e.g., the constants and operators in the expression).

- **Initialization**: You generate an initial population of 100 programs, all variations of f(x,y) (e.g., 2x2+y2, x2+2y, etc.).
    
    f(x,y)f(x, y)
    
    2x2+y22x^2 + y^2
    
    x2+2yx^2 + 2y
    
- **Selection**: You select the top 20 programs based on their scores (how well they optimize the problem).
- **Optimization**: You recombine subsolutions (e.g., change constants, switch operators) to generate new programs like 3x2+y or x+y2.
    
    3x2+y3x^2 + y
    
    x+y2x + y^2
    
- **Evaluation**: The new programs are scored and compared with the old ones.
- **Replacement**: Low-scoring programs are replaced with new, better programs.
- **Repeat**: This process repeats for 50 generations (G = 50), refining the population with each iteration until the algorithm converges on the best program.

---

### **Summary of G Iterations in MOSES**:

- MOSES iteratively improves a population of **N programs** over **G generations** through **selection**, **recombination**, and **evaluation**.
- In each generation, the algorithm **selects** promising programs, **optimizes** them by recombining subsolutions, generates new programs, and **updates** the population based on fitness.
- The process continues until convergence or a stopping criterion is met, leading to the discovery of the optimal solution.

This structure ensures that MOSES explores the program space efficiently, focusing on meaningful variations while gradually improving the population toward an optimal solution.