# Software Architecture

### The three big concerns:
- Function;
- Separatioon of components;
- Data management;

### Programming Paradigms
- Structure Programming: Imposes discipline on direct transfer of control;
    - Forces us to recursively decompose a program into a set of small provable functions;
- Oriented Programming: Imposes discipline on indirect transfer of control;
    - Allows us to use the plugin architecture. In which modules that contain high-level policies are independent of modules that contain low-level details. The low-level details are relegated to plugin modules that can be deployed and developed independently from other modules;
- Functional Programming: Imposes discipline upon assignment;
    - Race conditions, deadlock conditions and concurrent update problems are due to mutable variables.
    - In order to avoid these problems we should immutability but for that we need to make some compromises:
        - Segregation of mutability
            - Separate Immutable Components (pure functional way) from Mutable Components (not purely functional).
            - Since mutating state exposes these components to concurrency problems, it is commont practice to use some kind of transactional memory to protect mutable variables from concurrent updates and race conditions.
            - Push as much processing as possible into immutable components.

Any program can be constructed just from these three structures:
- Sequence;
- Selection;
- Iteration;
- Indirection;

'We prove we are correct by failing to prove incorrectness, despite our best efforts.'

