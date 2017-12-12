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
    - Technical
        - Select which architectural style will be used
            - Client Server
            - Message Bus
            - Service Oriented Architecture
            - Domain Driven Design
            - Layered Architecture
            - Component Based
        - Which architectural patterns to leverage
            - MVC
            - Publish/Subscribe
            - Peer-to-peer
        - Choose between purchasing or constructing a solution. It is the architect responsability to guide the enterprise on which path to follow;
        - Design a solution that solves business problem
            - Goals:
                - Solve the problem;
                - Understanding entire problem;
                - Creating technical solution;
            - This design should be technically and organizationally feasible;
                - Goals:
                    - Communicating the solution
                    - Technical and Non-technical stakeholders
                - Before drawing any solution, understand organizational business and technical tolerances;
                - Take into account when designing a solution:
                    - Team experience
                    - Project duration
                    - Cost
                    - Resourcing
                    - Deployed infrastructure
                    - Business process
                    - Technical team processes
                    - Methodologies
        - Document the architecture
        - Evaluate Architecture
            - Evaluate own architecture and peers architecture
            - Evaluation aspects:
                - How well the solution solves the problem;
                - Address quality attributes;
                - How it meets the projects and organization goals;
        
    - Non-Technical
        - Identify how a solution will achieve its business goals. This can be identified by:
            - Project scope and functional requirements;
            - Discussion with business stakeholders;
            - Present a high level architecture
                - This is where the architect interpretation of the business goals is presented;
            - Divide project into subsystems
                - Smaller workable chunks
                - Smaller teams working concurrently
- Why does an organization need software architects?
    - To mitigate risk
    - Most common reasons project fails:
        - Does not achieve business goals;
        - Takes too long;
        - Costs too much;
    - Architects bring:
        - Vision, leadership, structure and experience
    - Project estimates and duration
        - Feasibility is based on top down estimates;
        - Duration is based on bottom up estimates;
    - Define the Need vs. Want with business team;
    - Reduce time and cost
        - The architect should identify complex components and along with the business decide whether to keep or eliminate them;
        - More developers does not always help
    
### Project phases
- Initiation
    - First thing the architect/architects should do is to outline a viable solution;
        - Identify the most complex pieces of the solution;
            - Generally the most complex pieces are the ones that will interact with third party systems;
        - Identify portions that will most greatly impact timeline and cost (Architecturally significant portions of the project);
    - Project Sizing
        - Provide a high level cost and resource estimates so the business can decide whether the project is viable;
        - This is not an actuall estimation, but a general connotation that does not imply commitment;
        - Create bucket sizes
            - Small: <5 people / <6 months
            - Medium: 5-10 people / 3 to 12 months
            - Large: 25+ / 6-12+ months
    - Know the stakeholders
        - Organization leaders
        - Enterprise architects
        - Project managers
        - Business users
        - Understand their needs and goals
    - Know what questions to ask
    - Develop and maintain strong feedback loops
    - Technical vision document
        - It describes the overall plan/vision for the solution
            - It outlines the core requirements in a very high level, based on the key features;
            - Quality attributes, constraints, goals;
        
- Assembling the team
    - Architects, Senior Developers and Business domain experts;
    - Purposes:
        - Create a feedback loop of trusted domain and tech experts;
    - Let the team participate to the design process;
        
- Requirements
- Design
- Construction
- Testing
- Implementation

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
