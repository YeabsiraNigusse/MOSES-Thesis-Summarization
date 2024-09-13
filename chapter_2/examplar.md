# Examplar

An **exemplar** is a program (or a family of closely related programs) that acts as a **starting point** for further exploration. In MOSES, the algorithm creates **representations** centered around these exemplars to explore variations and generate new solutions. The exemplar serves as the **anchor** or **reference solution** for constructing **parameterized spaces** that capture meaningful variations in program behavior.

### How Exemplars Relate to Representation Building

Representation building revolves around the idea of constructing a **compact and meaningful subspace** of possible programs that are based on a specific exemplar. Here's how exemplars play a role:

### 1. **Starting Point for Representation**

- The exemplar is the **seed program** from which a set of **knobs** (parameters) are generated. These knobs control variations in the program’s behavior or structure.
- The goal is to create a **parameterized representation** around this exemplar, so small changes in the knobs lead to meaningful behavioral changes in the resulting programs. Essentially, the algorithm creates a search space of programs around the exemplar.

### 2. **Defining the Representation Space**

- The **representation** defines the **search space** for variations on the exemplar. By tweaking the knobs, the algorithm can explore different behaviors derived from the exemplar. This process is central to **competent optimization** because it focuses the search on meaningful variations rather than random mutations.
- For example, an exemplar program might have a set of operations, and the representation will allow the algorithm to adjust parameters (like constants or weights) that affect how the program behaves.

### 3. **Creating Subspaces for Search**

- **Representation-building** based on an exemplar constructs a **subspace** in the larger search space. This subspace is designed to capture **relevant program variations** while ignoring irrelevant ones.
- The goal is to create a **compact subspace** that focuses on important behavioral differences. By doing so, the algorithm can search more efficiently within this subspace rather than exploring the entire, vast program space.

### 4. **Refining and Exploring the Space**

- As the search progresses, MOSES may create new exemplars from the **best-performing programs** in a given representation space. Each new exemplar serves as the center of a new representation, allowing the search to move into different regions of the program space and explore **new promising areas**.
- This **adaptive representation building** helps refine the search by continuously generating new exemplars and their corresponding representations, guiding the optimization process.

### Key Points About Exemplars in Representation Building:

1. **Exemplars are Central**: The entire representation-building process starts with an exemplar, which defines the **scope** and **structure** of the search.
2. **Compact Subspace Creation**: By building representations around exemplars, the algorithm reduces the complexity of the search space, focusing only on **relevant variations**.
3. **Guided Search**: Instead of exploring the entire program space blindly, the search is **guided** around exemplars, making it more efficient and increasing the chances of finding **better solutions**.
4. **Adaptation**: As better solutions are found, they become new exemplars, allowing the search to **evolve dynamically** and adapt to new information.

### Example:

Imagine an exemplar program that computes a mathematical expression like 3×x+y3 \times x + y3×x+y. Representation building would focus on creating a **knob space** around this exemplar, allowing the algorithm to explore variations like changing the coefficients (e.g., 2×x+0.5×y2 \times x + 0.5 \times y2×x+0.5×y) or adding/subtracting terms, leading to new solutions that are **semantically meaningful** (i.e., that change the output behavior in important ways).

In MOSES, the starting point of the exemplar (the initial population of solutions) is generated from a simple or empty program or solution representation, which is the baseline. This baseline is typically predefined or randomly initialized. Here's how the process begins:

1. **Initial Representation**: The very first exemplar starts from a minimal or simple initial solution. This could be:
    - An empty program.
    - A basic set of operations or expressions predefined for the problem domain (e.g., simple logical operations in Boolean formulae or basic mathematical functions in numerical problems).
2. **Random Sampling**: Based on this initial representation, random variations are created to form the first generation of candidate solutions. This is where the first population is randomly sampled around the initial "empty" or basic solution:
    - MOSES uses "knobs" (parameters) to randomly generate diverse candidate solutions based on the initial exemplar.
    - These candidate solutions are then evaluated using the scoring function.
3. **First Exemplar**: The best-performing candidate solution from this initial random population (based on the scoring function) becomes the first exemplar. This solution serves as the basis for further representation-building and search within the program space.
4. **Dynamic Representation Building**: Once the first exemplar is chosen, MOSES constructs a new parameterized representation (i.e., builds "knobs" around this solution) and continues the search by exploring variations within this new space.