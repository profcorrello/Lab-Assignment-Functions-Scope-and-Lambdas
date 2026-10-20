# Markdown Description
This application is a comprehensive, single-file sample designed for an "Intro to Python" course, covering advanced topics including Functions, Scope, Lambda Expressions, and Functional Programming paradigms.

The script is structured into logical sections to demonstrate each concept clearly:

1.  **Basic Functions & Scope**: Demonstrates defining reusable functions using `def`, proper docstrings, and type hinting. It illustrates local scope by defining a variable inside a function that cannot be accessed globally.
2.  **Advanced Function Signatures**: Shows how functions handle variable arguments using `*args` (collects excess positional arguments into a tuple) and `**kwargs` (collects excess keyword arguments into a dictionary). It also demonstrates the flexible use of positional and keyword arguments.
3.  **Lambda and Functional Tools**: Introduces `lambda` expressions for concise, single-line operations. It then utilizes `map`, `filter`, and `functools.reduce` to perform data transformations in a functional, declarative style.
4.  **Tuple Packing and Unpacking**: Demonstrates Python's ability to return multiple values (a tuple) from a function using comma separation and how these values can be cleanly assigned to multiple variables upon calling (unpacking).
5.  **Closures (Stateful Lambdas)**: Implements a factory function (`make_multiplier`) that generates specialized lambda functions. This demonstrates a closure, where the inner function retains access to the outer function's variable (`factor`) even after the outer function has finished executing.
6.  **Scope Management (Early Exit)**: Simulates a search algorithm within nested loops, demonstrating that using a `return` statement provides an efficient "Instant Loop Exit," immediately terminating the entire function regardless of the loop nesting, which is critical for performance.

**Setup/Execution:**
This script requires only a modern Python 3.12 environment. Copy the entire code block and run it directly. The output will clearly guide the user through the execution and result of each demonstrated concept.

# Code Sample
```python
"""
Intro to Python: Functions, Scope, and Lambda Expressions
A comprehensive module demonstrating advanced Python concepts (Python 3.12+).
"""

import functools
from typing import List, Dict, Any, Tuple

# ==============================================================================
# 1. BASIC FUNCTIONS, TYPE HINTING, AND SCOPE
# ==============================================================================

def calculate_total(price: float, tax_rate: float, quantity: int = 1) -> float:
    """
    Calculates the final total price including tax.

    This function demonstrates:
    1. Type Hinting: Ensures parameters and return values are predictable.
    2. Docstrings: Provides clear documentation of purpose, parameters, and return value.
    3. Default Arguments: 'quantity' defaults to 1.

    Args:
        price: The base unit price.
        tax_rate: The tax rate (e.g., 0.05 for 5%).
        quantity: The number of units purchased (optional).

    Returns:
        The final calculated total price.
    """
    total = price * (1 + tax_rate) * quantity
    return total

def demonstrate_scope(global_data: str) -> None:
    """
    Demonstrates variable scope (Global vs. Local).
    """
    # Local variable defined within the function's scope
    local_message: str = "This message is local to the demonstrate_scope function."
    print("\n--- Scope Demonstration ---")
    print(f"Inside function (Local): {local_message}")
    print(f"Accessing Global variable: {global_data}")
    
    # Note: Trying to access 'local_message' outside this function will raise a NameError.
    # This illustrates that local scope variables are isolated.

# ==============================================================================
# 2. ADVANCED FUNCTION SIGNATURES (*args, **kwargs)
# ==============================================================================

def summarize_user_data(
    user_id: int, 
    name: str, 
    *args: str, 
    **kwargs: Any
) -> str:
    """
    A flexible function accepting variable arguments (*args and **kwargs).

    Args:
        user_id: Required positional argument (int).
        name: Required keyword argument (str).
        *args: Collects any extra positional strings into a tuple.
        **kwargs: Collects any extra keyword arguments into a dictionary.

    Returns:
        A summary string of the input data.
    """
    print("\n--- *args and **kwargs Demonstration ---")
    print(f"1. User ID (Positional): {user_id}")
    print(f"2. Name (Keyword): {name}")
    print(f"3. Extra Positional Args (*args) (Tuple): {args}")
    print(f"4. Extra Keyword Args (**kwargs) (Dict): {kwargs}")
    
    return f"Summary created for {name} (ID: {user_id}). Processed {len(args)} extra args and {len(kwargs)} extra flags."

# ==============================================================================
# 3. LAMBDA AND FUNCTIONAL PROGRAMMING (map, filter, reduce)
# ==============================================================================

def functional_data_processing(numbers: List[int]) -> None:
    """
    Demonstrates functional utilities: lambda, map, filter, and reduce.
    """
    print("\n--- Lambda and Functional Programming Demonstration ---")
    
    # --- Lambda Basics ---
    # 1. Anonymous function for squaring a number.
    square_lambda = lambda x: x * x
    print(f"Lambda Example (Square 4): {square_lambda(4)}")

    # --- Map Function ---
    # Applies a function (lambda) to every item in an iterable.
    # Goal: Square every number in the list.
    squared_list = list(map(square_lambda, numbers))
    print(f"Map Result (Squared List): {squared_list}")
    
    # --- Filter Function ---
    # Keeps only elements that satisfy a given predicate (lambda).
    # Goal: Keep only even numbers.
    even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
    print(f"Filter Result (Even Numbers): {even_numbers}")

    # --- Reduce Function ---
    # Applies a rolling computation (lambda) to a sequence, reducing it to a single value.
    # Goal: Calculate the product of all numbers.
    product = functools.reduce(lambda acc, x: acc * x, numbers)
    print(f"Reduce Result (Product): {product}")

# ==============================================================================
# 4. TUPLE PACKING AND UNPACKING
# ==============================================================================

def calculate_metrics(data: List[float]) -> Tuple[float, float, float]:
    """
    Calculates sum, count, and average.
    Returns multiple values, Python automatically packs them into a tuple.
    """
    total_sum = sum(data)
    count = len(data)
    average = total_sum / count if count > 0 else 0.0
    
    # Tuple Packing: Returning multiple comma-separated values
    return total_sum, count, average

def demonstrate_packing_unpacking(data: List[float]) -> None:
    """
    Demonstrates tuple packing (return) and unpacking (assignment).
    """
    print("\n--- Tuple Packing and Unpacking Demonstration ---")
    
    # Packing happens here (return values become a tuple)
    total, count, avg = calculate_metrics(data)
    
    # Unpacking happens here (assigning tuple elements to individual variables)
    print(f"Data analyzed: {data}")
    print(f"Total Sum (Unpacked): {total:.2f}")
    print(f"Count (Unpacked): {count}")
    print(f"Average (Unpacked): {avg:.2f}")


# ==============================================================================
# 5. CLOSURES (Stateful Lambdas)
# ==============================================================================

def make_multiplier(factor: int) -> Any:
    """
    A factory function that creates a specialized lambda (closure).
    The returned lambda 'remembers' the 'factor' value from its enclosing scope.
    """
    print("\n--- Closure Demonstration ---")
    print(f"Factory initiated with factor: {factor}")
    
    # The returned lambda "closes over" the 'factor' variable.
    return lambda x: x * factor

def demonstrate_closure() -> None:
    """
    Demonstrates state retention using a closure.
    """
    # 1. Create a specialized function that always doubles its input
    double_it = make_multiplier(2)
    
    # 2. Create another specialized function that always triples its input
    triple_it = make_multiplier(3)
    
    print(f"Result of calling 'double_it' (2 * 5): {double_it(5)}")
    print(f"Result of calling 'triple_it' (3 * 5): {triple_it(5)}")
    print("The lambda functions retain the state (factor) even after make_multiplier finished.")


# ==============================================================================
# 6. SCOPE MANAGEMENT: INSTANT LOOP EXIT
# ==============================================================================

def search_matrix(matrix: List[List[int]], target: int) -> bool:
    """
    Searches a nested list (matrix) for a target value.
    Uses 'return' to achieve an efficient 'Instant Loop Exit' upon finding the target.
    """
    print("\n--- Scope/Control Flow (Instant Loop Exit) Demonstration ---")
    rows = len(matrix)
    if rows == 0:
        return False

    for i in range(rows):
        print(f"Checking Row {i}...")
        for j in range(len(matrix[i])):
            if matrix[i][j] == target:
                print(f"SUCCESS: Target {target} found at position ({i}, {j}).")
                # CRITICAL: Returning here immediately exits BOTH loops and the function, 
                # saving computation time.
                return True
    
    print(f"FAILURE: Target {target} not found in the matrix.")
    return False

# ==============================================================================
# MAIN EXECUTION BLOCK
# ==============================================================================

if __name__ == "__main__":
    # --- 1. Initial Setup and Scope Test ---
    print("=========================================================")
    print(" PYTHON INTRO COURSE: FUNCTIONS, SCOPE, & LAMBDA ")
    print("=========================================================")
    
    # Demonstrate Scope
    demonstrate_scope(global_data="The global variable is accessible here.")

    # Demonstrate basic function usage
    price_a = 100.00
    tax_a = 0.05
    print("\n--- Function Usage Example (calculate_total) ---")
    total_1 = calculate_total(price_a, tax_a)
    print(f"Total for 1 item: ${total_1:.2f}")
    
    # Demonstrate default and positional/keyword arguments
    total_2 = calculate_total(price_a, tax_a, quantity=5)
    print(f"Total for 5 items (using keyword arg): ${total_2:.2f}")
    
    # --- 2. Advanced Arguments Demonstration ---
    user_summary = summarize_user_data(
        user_id=101, 
        name="Alice Smith", 
        "Student", 
        "Gold", 
        department="CS", 
        enrollment_year=2022
    )
    print(f"Result: {user_summary}")

    # --- 3. Functional Programming Demonstration ---
    data_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    functional_data_processing(data_list)

    # --- 4. Tuple Packing and Unpacking Demonstration ---
    demonstrate_packing_unpacking(data_list)

    # --- 5. Closure Demonstration ---
    demonstrate_closure()

    # --- 6. Scope/Control Flow Demonstration ---
    matrix = [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]
    ]
    
    # Case 1: Find an element (triggers early exit)
    search_matrix(matrix, 5)
    
    # Case 2: Element not found (runs through all loops)
    search_matrix(matrix, 99)
```