# Minimum-Registers-Required-using-Labelling-Algorithm-CD-Project
Aim: Construct a DAG with visualization and find the minimum number of registers using labelling algorithm.

------------------------------------------------------------------------------------------------------------------------------------------------------------------
Purpose:
The function generate_tac takes an expression (like "X - Y + X * Y * U - V / W + X + V") and generates Three Address Code (TAC), which is a simpler intermediate representation of the expression, used for optimization and code generation.

Steps:
Tokenize the expression:
The function splits the input expression into smaller pieces called "tokens" using a regular expression (re.findall).
It breaks down the expression into variables (X, Y, U), numbers, and operators (+, -, *, /), and parentheses.
Initialize Data Structures:
temp_count: Keeps track of the temporary variable names (e.g., T1, T2).
stack: A temporary stack used for operator precedence.
output: A list where we will store the final expression in "postfix" order (i.e., operators come after operands).
tac: A list to store the final Three Address Code.
temp_vars: A dictionary to store intermediate results for each temporary variable.

Convert the expression to postfix (Reverse Polish Notation):
It loops through the tokens and handles operators and operands. The goal is to arrange the expression in postfix order so that operators appear after their operands.
Parentheses are used to prioritize operations, and the stack is used to handle operator precedence.

Generate TAC:
Once the expression is in postfix form, the function processes each token:
If it's a number or variable, it's added to the stack.
If it's an operator (like + or *), it pops two operands from the stack, creates a temporary variable (e.g., T1), and writes a line of TAC like T1 = op1 + op2.
The temporary variable T1 is then pushed back onto the stack.
This process continues for all tokens in the postfix expression.

Final result:
Once all tokens are processed, the final result is stored in the Z variable, which is the last line of the TAC (Z = Tn, where Tn is the last temporary variable).

------------------------------------------------------------------------------------------------------------------------------------------------------------------

DAG Creation & Visualization

create_dag(temp_vars):
Builds a Directed Acyclic Graph (DAG) from TAC intermediate steps.
Adds nodes for operations (+, -, *, /) and connects operands.
Reuses nodes for repeated operations to optimize the graph.
Adds a final node Z representing the result.

draw_dag(G):
Uses Graphviz layout to arrange nodes in a tree-like structure.
Colors nodes, adjusts labels, and visualizes dependencies between operations.
Displays the DAG, showing the computation flow from operands to the final result.

------------------------------------------------------------------------------------------------------------------------------------------------------------------
The register_allocation(G) function assigns registers to nodes in a Directed Acyclic Graph (DAG). It iterates through the graph in topological order, assigning registers based on the following:
Root nodes get alternating registers.
Nodes with one predecessor inherit its register.
Nodes with two predecessors take the higher register or a new one if both share the same register. Finally, it calculates the minimum number of registers needed by finding the highest register used.
