# Detail view

The challenges discussed in Section 2.1.2 relate to how difficult it is to build **representations** (i.e., models or structures) that accurately capture important **semantic** (behavioral) variations while avoiding getting trapped in irrelevant **syntactic** (structural) differences. Let’s break down the specific challenges:

### 1. **Non-Orthogonality (Redundancy)**

- **The Problem**: In programming, the same operation can be written in many different syntactic ways. For example, due to **commutativity** and **associativity**, a1+a2+...+an can be rearranged into countless forms that all mean the same thing. Similarly, adding zero or multiplying by one doesn't change the behavior, but creates **different syntactic forms**.
    
    a1+a2+...+ana_1 + a_2 + ... + a_n
    
- **Why It's a Challenge**: This creates **redundancy** in the search space. The same behavior can appear under many syntactically different forms, causing **over-representation**. This makes the search space much larger and harder to explore efficiently because the algorithm is forced to deal with many versions of the same solution.
- **Impact on Representation Building**: To build an effective representation, you want to focus on **important variations** in the program's behavior (semantics) and **ignore unimportant syntactic variations**. However, this redundancy makes it difficult to reduce the space to only meaningful representations, which slows down the search.

### 2. **Oversampling of Distant Behaviors**

- **The Problem**: Programs that are **behaviorally very different** (i.e., their outputs change significantly with minor input changes) tend to be over-represented during the search. This is partly due to the chaotic nature of program execution, where small syntactic changes can lead to wildly different behaviors.
- **Why It's a Challenge**: This causes the algorithm to spend too much time evaluating programs that are **very different from each other** when minor changes might lead to better results.
- **Impact on Representation Building**: The goal of representation building is to create compact, useful subspaces to explore. If the algorithm spends too much time on distant, irrelevant behaviors, it can miss promising areas of the search space that are **behaviorally similar** but **semantically useful**.

### 3. **Undersampling of Nearby Behaviors**

- **The Problem**: Programs that are **syntactically different** but behave similarly can get **undersampled** (not explored enough). For example, both 3×x and x+x+x compute the same thing, but if the algorithm only looks at one form, it might miss similar variations that could be useful.
    
    3×x3 \times x
    
    x+x+xx + x + x
    
- **Why It's a Challenge**: This leads to missed opportunities for optimization because the algorithm fails to explore **small variations** in behavior that might improve the solution.
- **Impact on Representation Building**: If the algorithm doesn’t explore nearby behaviors enough, it won’t discover **fine-grained improvements** in program performance, making the representation less effective in covering the most promising subspaces.

### Key Takeaway:

These challenges highlight how **syntactic variation** (how a program is structured) can mislead the search process, making it harder to focus on **semantic variation** (how a program behaves). **Representation building** must overcome these problems by:

- Reducing **redundancy** (non-orthogonality) to simplify the search space.
- Avoiding the trap of focusing too much on **distant behaviors**.
- Ensuring enough exploration of **similar but subtly different** behaviors (nearby behaviors).

MOSES addresses these challenges by trying to focus on **behavioral variations** rather than syntactic ones, ensuring that the search process is more **efficient** and **effective** at finding meaningful solutions.