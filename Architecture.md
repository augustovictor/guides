# Software Architecture

### Initial questions
- Who is a software architect?
    - Technical expert
    - Good communicator and listener
    - Collaborator
    - Workflow begins with an idea that must be heard and understood. Then Synthesized through communication and collaboration across the organization. And finally trascripted to an architecture along with the stakeholders, based on their needs and goals.
        - Stakeholders:
            - Developers
            - Project management
            - Quality assurance
            - Change management
            - Marketing
            - Business
            - Executive
            - Customers
        - The architect goal here is to collaboratively work with all the groups involved to agree on a design and facilitate the construction of the solution.
- What is an architect expected to be skilled at?
    - Technical
        - Developer
        - Designer
        - Modeling
        - Keep up new techs
        - Architectural concepts
            - Architectural patterns
            - Architectural styles
        - Design patterns
        - Software engineering
        - Software Design
        - Programming
        - Platform knowledge
    - Non-Technical
        - Business processes
        - Business and enterprise domain
        - Management
            - Project management
            - Problem solving
            - Negotiation
            - Facilitation
        - Leadership
            - Vision
            - Self directed
            - Decisive
            - Motivational
            - Inspirational
            - Confident
            - Committed
            - Know how to delegate
            - Be positive and creative
- Types of architect
    - Enterprise Architect (More aligned with business than tech)
        - Strategic Architect
            - Concerns:
                - People
                    - Build and/or organize a team
                    - Break solutions into manageable pieces
                    - Deliverable order
                - Process
                    - Develop your own processes
                    - Create a set of repeatable procedures
                - Information Flow
                - Business Processes
                - Strategic goals
                - Make sure business and technical strategies align
                - Roadmaps
    - Solutions Architect (Technical architect)
        - Cross Domain
        - Cross-functional
        - Systems Interactions
        - Frameworks
        - Infrastructure
        - Interoperability
        - Horizontal Problems
            - Roadmaps
            - Guidance
        - Cross cutting concerns
            - Reuse
            - Process
            - Guidance
        - Strategic Solutions
    - Application Architect (Operational Architect)
        - Focused on a single application (or vertical)
        - Single technology (web, desktop or mobile)
        - Component reuse
        - Maintainability
        - Detailed design for their problem domain
        - Components, Modules, Classes, Libraries, Languages
        - Reuse with business unit
- What is an architect expected to do?
    - Technical & Non-Technical
- Why does an organization need software architects?

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

## Expectations of a software architect
- Analyze technology, industry, and market trends and keep current with those latest trends;
- ( Core thing ) Analyze the current technology environment and recommend solutions for improvement;
- Ensure compliance with the architecture
    - Create checkboxes and stuff so people know what they have to comply with;
- Have exposure to multiple and diverse technologies, platforms, and environments;
- Possess exceptional interpersonal skills, including teamwork, facilitation, and negotiation;
- Define the architecture and design principles to guide technology decisions for the enterprise;
- Understand the political climate of the enterprise and be able to navigate the politics;

## Architecture aspects
- Leadership and communication
- Techinal knowledge
- Business domain knowledge
- Methodology and strategy

## Is X an architectural question?
- To find the answer we have to consider Type X Implementation

## Antipattern
- Choose technology first and then build the architecture around it;

### Soft Skills
- 
