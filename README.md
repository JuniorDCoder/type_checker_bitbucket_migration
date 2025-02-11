Here’s a detailed README file for your code:

---

# Type Checker for Toy Programming Language

This program is a type checker for a simplified toy programming language. It analyzes a program written in the toy language, checks for type errors, and provides detailed feedback.

---

## Table of Contents

1. [Overview](#overview)
2. [Features](#features)
3. [Input Format](#input-format)
4. [How It Works](#how-it-works)
5. [Code Explanation](#code-explanation)
6. [Error Handling](#error-handling)
7. [How to Run](#how-to-run)
8. [Examples](#examples)
9. [Future Enhancements](#future-enhancements)

---

## Overview

The type checker validates the following aspects of a toy program:

- Variable declaration and assignment.
- Type compatibility during assignments.
- Basic support for conditional statements.
- Binary operation type checking.

It processes a file named `toy_program.txt` and reports errors like undeclared variables, type mismatches, and unsupported types.

---

## Features

- **Symbol Table**: Keeps track of declared variables and their types.
- **Type Validation**: Ensures type compatibility between variables and assigned values.
- **Conditional Statement Recognition**: Identifies conditional structures.
- **Error Reporting**: Highlights issues such as type mismatches or undeclared variables.

---

## Input Format

The program reads lines of code from a file named `toy_program.txt`. Supported statements include:

1. **Variable Declaration and Assignment**:

   ```plaintext
   <type> <variable> = <value>;
   ```

2. **Assignment**:

   ```plaintext
   <variable> = <value>;
   ```

3. **Conditionals**:
   ```plaintext
   if (<condition>) {
       <statements>
   }
   ```

**Note**: The toy language assumes a simplified structure and does not evaluate complex expressions.

---

## How It Works

1. **Read Program File**: Line-by-line processing of `toy_program.txt`.
2. **Symbol Table Management**: Tracks declared variables and their types.
3. **Type Checking**:
   - Matches variable types during assignments.
   - Infers types of expressions (e.g., `true` -> `BOOL`, `3.14` -> `FLOAT`).
4. **Error Reporting**: Detects and reports undeclared variables and type mismatches.

---

## Code Explanation

### 1. **Type Enumeration**

```c
typedef enum
{
    INT,
    FLOAT,
    BOOL,
    STRING,
    VOID
} Type;
```

Defines the supported types: `INT`, `FLOAT`, `BOOL`, `STRING`, and `VOID`.

---

### 2. **Symbol Table**

```c
#define MAX_SYMBOLS 100
Symbol symbolTable[MAX_SYMBOLS];
int symbolCount = 0;
```

The symbol table stores up to 100 variables with their names and types.

---

### 3. **Core Functions**

#### `addSymbol`

Adds a new variable to the symbol table.

```c
void addSymbol(char *name, Type type)
```

#### `lookupSymbol`

Searches for a variable in the symbol table and returns its type.

```c
Type lookupSymbol(char *name)
```

#### `checkAssignment`

Validates that the type of an expression matches the type of a variable.

```c
void checkAssignment(char *varName, Type exprType)
```

#### `checkBinaryOperation`

Checks type compatibility for binary operations.

```c
Type checkBinaryOperation(Type left, Type right, char *op)
```

#### `getTypeFromString`

Converts a string representation of a type into its enumerated value.

```c
Type getTypeFromString(char *typeStr)
```

#### `getTypeFromExpression`

Infers the type of an expression based on its format.

```c
Type getTypeFromExpression(char *expr)
```

#### `processLine`

Processes a single line of code, handling variable declarations, assignments, and conditionals.

```c
void processLine(char *line)
```

---

### 4. **Main Function**

The `main` function reads the file, processes each line, and handles errors.

```c
int main()
```

---

## Error Handling

1. **Undeclared Variables**:

   - Reported when a variable is used without being declared.
   - Example:
     ```plaintext
     Error: Variable 'x' not declared.
     ```

2. **Type Mismatches**:

   - Occurs when a variable is assigned a value of an incompatible type.
   - Example:
     ```plaintext
     Type Mismatch Error: Cannot assign 1 to 0 for variable 'x'.
     ```

3. **Unsupported Types**:

   - Reported for types not recognized by the system.
   - Example:
     ```plaintext
     Error: Unknown type 'char'.
     ```

4. **Unprocessed Lines**:
   - Highlights unsupported syntax.
   - Example:
     ```plaintext
     Error: Could not process line '...'.
     ```

---

## How to Run

1. **Create Input File**: Write your program in `toy_program.txt`.
   Example:

   ```plaintext
   int x = 5;
   float y = 3.14;
   x = 10;
   if (x > 5) {
       y = 2.71;
   }
   ```

2. **Compile the Program**:

   ```bash
   gcc typechecker.c -o typechecker
   ```

3. **Run the Program**:
   ```bash
   ./typechecker
   ```

---

## Examples

### Input

```plaintext
int x = 10;
float y = 3.14;
x = 20;
if (x > 10) {
    y = 2.71;
}
}
```

### Output

```plaintext
Processing conditional: if (x > 10) {
Error: Could not process line '}'.
```

---

## Future Enhancements

- Support for more complex expressions.
- Nested conditionals and loops.
- Enhanced binary operation type inference.
- Extend the language to support arrays and functions.

---

## Contributing

Feel free to suggest improvements or report issues. Submit pull requests for feature additions or bug fixes.

---

## License

This project is open-source and licensed under the [MIT License](LICENSE).