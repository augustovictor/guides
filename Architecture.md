# Software Architecture

### Initial questions
- What are the software architecture goals?
    - To minimize the required human resources to develop and maintain a system;
    - To identify structures, their elements, relationships between them, and how thei interact with each other. Properties and behaviors (interactions) must be identified;
        - Elements
        - Relations
        - Properties
        - Behavior
- What are the architectural design goals?
    - Separate large problem domains into manageable pieces;
    - Abstract and encapsulate complexities of the problem at hand;
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
            - Architectural patterns (Deal with structure and organization of the entire system or subsystems)
            - Architectural styles
        - Design patterns (Solve problems well understood during construction)
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
    - Functional requirements (What the system shall do (Not how to implement))
        - Architect plays a supportive role
        - A good functional requirement describes:
            - Input
            - Behavior
            - Output
    - Non-functional requirements (What the system shall be)
        - Identify these requirements first
        - Architect plays a more active role
        - This kind of requirements are the ones that impact the architecture;
        - Some of the non-functional requirements are the cross cutting concerns and quality attributes;
        - Examples of non-functional requirements (Quality attributes list):
            - Accessibility
            - Availability
            - Configurability
            - Extensibility
            - Performance
            - Maintainability
            - Scalability
            - Security
            - Supportability
            - Testability
            - Usability
        - Questions to ask to find answers on non-functional requirements:
            - How many users are expexted to use the system initially?
            - What will this grow to in the future?
            - What will the business impact be if the system is unavailable?
        - Identify constraints:
            - Constraints are put there to guide the team and mitigate risks by providing vision with clear goals;
            - Time
            - Resource
            - Budget
            - Team skills
            - Deployed infrastructure
            - Standards
                - Architectural
                - Technology
                - Coding
- Design
    - Here is when the architect creates a design that meets the needs of the business;
    - It is the process that focus on understanding and defining structures taht make up the solution. Whereas Documentation is the process of communicating the solution externally to an audience;
    - There will be mistakes and the key is making them less expensive to change. It is an iterative process;
    - Identify the portions of the solution that are most likely to change and design a solution to mitigate these risks;
        - Risky portions often occur at boundaries;
        - It is a good idea to develop a high level design with a small group of people and a more detailed one with more experienced developers;
        - Things to keep in mind when selecting the design team:
            - This is not a place for junior developers
        - Design sessions workflow:
            - Begin with brainstorming;
            - The team does not have to understand every little aspect of the problem, but the whole problem that is being solved;
            - Create Views that communicate structures to an audience
                - Views are representations of the design to a particular audience.
                    - Some views target business;
                    - Some views target technical;
                    - Some views target both;
                - Each view represents a single perspective of the solution to THAT audience;
                    - In this case views are windows into your design;
                    - No single viewpoint represents the entire solution;
    
- Construction
    - The architect organize the project into logical segments;
    - The architect must train the team to get them up to speed;
    - Stay one step ahead of development effort;
    - Review functional requirements to make sure assumptions made in the beginning of the project still hold true (Design validation);
        - If there will be any change the architect must provide technical direction to the team;
    - The architect should decide with the team:
        - Unit testing requirements;
        - Change management practices;
        - Coding standards;
        - Source code pository;
    - Code review should be an integrap part of the process;
- Testing
    - Quality assurance testing (Architect plays a supportive role)
        - Help testers to understand requirements;
        - Help to translate requirements into test cases;
        - Make sure quality assurance environment exists and it is being used;
    - Performance testing (Architect plays an active role)
        - Make sure there is an environment similar to production;
- Implementation
    - Help coordinate deployment;
    - Work with infra team to decide whether a new infra has to be created or an existing one can be used;
        - If the deployment will be done to an existing infra, then it should be identified as an architectural constraint;
    - Make sure health checks and performance monitors are in place;
    - 3 Main areas of concern
        - Source code management (Git)
        - Build management
        - Deployment
    - Once the deploy is done, the architect should remain available for troubleshooting if needed;
    
### Detailed design vs Architecture design
- Design considerations:
    - What are the goals and objectives of your architecture?
    - What style of application will best meet your needs? Mobile, web, service oriented?
    - What are the architectural significant requirements that should be considered? And how does this design account for them?
    - What are the important system, run-time, design and user quality attributes of the solution? And how these addresses in your architecture?
    - Do any of these attributes have competing goals?
    - Which attributes are more important and what are the tradeoffs that should be considered?
    - What are the technical concerns of the solution?
    - Have you accounted for cross cutting concerns?
    - Will you utilize existing frameworks or create one as part of your project?
    - What patterns should be considered?
    - Have you considered technology, team, deployment and time constraints?
    - Are there alternative architecutres that should be considered?
    
### Architecture design (High level architecture)
- Is Iterative, layered and begins by defining the highest level of detail;
- Make everyone speak the same language;
- Define common set of terms;
    - Each term defines an element and a hierarchy;
    - Example of terms:
        - System
            - Highest level of detail and defines the entire scope of the project;
            - Made up of one or many subsystems;
        - Subsystem
            - Logical separation of responsability within the system boundary;
            - Grouping of related elements that comprise the entirety of your solution;
            - Sometimes can be a sandalone application that is part of the solution;
        - Module
            - Dedicated to a single logical area of responsability;
            - Grouping of other modules or components;
            - Responsabilities are easyily understood by team;
        - Component
            - Execution units in our solution;
            - Independently deployable software;
            - Designed to be pluggable;
            - Should be loosely coupled;
            - Defined by their interfaces and behaviors;
- Focus on the pieces that are difficult and costly to change;
- Architectural design is performed until it reaches the point where the development team can begin their work;
- Should rarely change. Since changes on this level are costly and painful;

#### Detailed design (Addresses implementation)
- Continues long after the architectural design is complete. The design is complete only when the project is delivered;
- Architecturally significant design choices are the ones that have wide impact on the solution;
- Meet non-functional requirements;
- Guide downstream design activities;
- Approaches to design and their benefits:
    - Common goals:
        - Create a set of common terms that can be used to facilitate communication between stakeholders;
        - Provide a representation of functional components;
        - Create a model that facilitates the partitioning of the problem domain;
    - Top-down (Traditional approach)
        - Highest level of abstraction, progressively work downward providing more details;
        - The goal is to break down the system into components with inputs and outputs;
        - It is performed iteratively as a series of sequential decomposition exercises;
            - In the end we would have a series of black boxes, interfaces and relationships between them. These are used as basis for implementation choices;
        - Benefits:
            - Provides a logical and systematic approach;
            - Helps to reduce size, scope, complexity of each module, which is benefitial for system partitioning, separation of concerns, and resource alocation;
            - Works for both functional and object oriented design approaches;
        - Disadvantages:
            - Requires an in depth understanding of the problem domain;
    - Bottom-up
        - Focus on the components that makeup the solution, working upward to assemble them into a whole. Like assembling lego pieces;
        - Benefits:
            - Allow the team to begin coding and testing early;
            - Since the team only builds what it needs the complexity of the design is reduced;
            - Promotes code reuse;
            - Promotes the use of continuous integration and unit testing to maintain quality and identify emergent issues;
        - Disadvantages:
            - Can be difficult to maintain;
    - Some common names are:
        - Up-front vs evolutionary design;
        - Decomposition vs composition;
        - Planned design vs emergent design;
    - It is possible to use both approaches.
        - Use the top-down approach during project inception;
    
        
#### Architectural Design Process - HLA (High Level Architecture)
- Defines:
    - System boundaries
    - External interoperation points
    - Subsystems
    - Subsystems types
    - Subsystems interoperation points
    - Modules
    - Responsabilities
- The HLA will be used to validate, set constraints and provide structure to the remaining design steps;
- STEP 1 - Start with the big picture and know your boundaries:
    - Considerations (These considerations are important to know what your solution responsabilities are, and how it will function as part of your organization ecosystem):
        - The first level of the architectural design defines your application boundaries and interoperation points with other applications. Both internal and external to the organization;
        - Where does your solution fit into your organization's ecosystem?
        - Will this solution interoperate with other systems withing your organization or will it be a standalone application that provides one simple function?
        - Will other applications use the database you're creating?
        - Will your application provide or consume any services?
        - Will your application access databases that are not part of your solution?
        - Take note of all systems that your solution will interact with and how they will communicate. Boundaries are an important consideration when designing a solution;
        - Boundaries create context so use that to focus on one problem at a time;
- STEP 2 - Define subsystems (Inventory of all subsystems, understanding of their responsabilities and how they interact with each other or an external system):
    - Identify subsystems;
    - If your solution contains many architecture types (Web, Mobile, services...) it is likely subsystems will be partitioned by application type.
        - If the subsystems interact with each other, and how they communicate.
- STEP 3 - Identify all modules that make up each subsystem
    - Modules will be defined for every subsystem proceeding horizontally from one subsystem to the next;
    - Interoperation between modules is important but we should stay within the boundaries of the subsystem;
- STEP 4 - Define components
    - Define components that make up or map each module;
    - Lower levels of design should be performed by development team;

#### Communicating the design to stakeholders (Technical and Non-Technical)
- Design and documentation are distinct processes with different goals;
    - Design identifies all the structures that make up the solution;
    - Documentation communicates design structures;
- Artifacts are representations of the architecture. They are created to communicate information to a particular audience;
- The size of the team will determine the number of details needed for each document;
- On small teams creating lots of design documents will not provide as much value as in large teams;
    - Small: up to 5;
    - Large: More than 5;
- Time spent in documenting pales in comparison to time spent:
    - Communicating the design;
    - Educating new team members;
    - Justifyiing and explaining design decisions;
- Artifacts can do this for you. It scales as your team grows;
- Main objectives for creating architectural artifacts:
    - OBJECTIVE 1: Facilitate communication between stakeholders
        - Communicate what is being built;
        - How functional and quality related requirements are being achieved;
        - Communicate system constraints;
        - These blueprints serve as the interface between the technical and non-technical stakeholders;
        - Define the structures from top-down and bottom-up;
        - Define the terms upon which the team will communicate;
    - OBJECTIVE 2: Basis for detailed design and construction efforts;
        - Provide the foundation upon which non-architectural, more detailed designs and construction will be built;
        - Architectural artifacts should provide guidance, structure and constraints that leads the team to meet the business goals;
    - OBJECTIVE 3: Educate the team, both business and technical
        - Facilitate duscussions;
        - Provide background;
        - Explain choices;
        - Document decisions;
        - Provide context and abstraction;
    - How do we know we are meeting these objectives?
        - Ask these two questions everytime you're creating an artifact:
            - Does this document provide value in at least one of the areas identified as objectives?
            - Does this level of detail communicate enough?
                - Is there enough detail for our business users to understand how we are meeting their needs?
                - Is there enough detail for our dev team to build a solution?

#### Documentation Standards
- Focus on diagrams;
- Types of diagrams:
    - Formal: UML
        - There are 14 types of UML diagrams which are divided into 2 categories:
            - Structural: Structures that make up the application;
            - Behavioral: Behavior and functionality;
                - Interaction: Represent the control flow between components;
    - Informal
        - Consists in boxes and lines that represent elements, relations and behavior;
    - Hybrid
        - Use of UML diagrams in conjunction with box and lines diagrams;
- Martin Fowler - 3 modes of UML diagrams
    - Sketch (Most common) - Does not necessarily conform to all the rules of UML. It focuses more on communicating concepts and ideas;
    - Blueprints (More formal);
    - Programming Language

#### What are views?
- Is a view into the architecture that has a single viewpoint targeted to a particular audience and addresses a specific set of concerns;
- Approaches
    - 4+1 architectural view model (5 views. Each address a separate set of concerns and audience):
        - Logical: End user functionality viewpoint (Class diagram)
            - Structures of the architecture that implement functional requirements;
            - Classes and their relationships;
        - Development (Package and component diagram)
            - Structure and organizational viewpoint
            - How modules are organized and how they interact;
        - Process (Activity diagram)
            - Run-time viewpoint
            - Performance
            - Reliability
            - Scalability
            - Interaction and communication
        - Phisical or deployment (Deployment diagram)
            - Infrastructure viewpoint
            - Where the solution will be deployed;
            - Communication between phisical tiers;
        - Use case (Scenario): Ties all views together (Use case diagram)
            - User requirements;
            - System functionallity;
            - Internal and external actors;
    - Views & Beyond (3 view categories) (2nd edition)
        - Module (Structural view of the architecture)
            - Addresses how modules are organized and how they interact with each other;
            - Provides a blueprint of the system that are often represented by decomposition diagrams;
            - Show dependencies between modules and the layers within a module;
            - Styles used when creating module views (Can be combined):
                - Decomposition
                - Uses
                - Generalization
                - Layered
                - Aspects
                - Data model
        - Component & connector (Behavioral view of the architecture)
            - Addresses how the elements of the system work together at run-time;
            - How they meet performance, reliability and availability quality attributes
            - Styles used when creating component & connector views:
                - Data flow
                - Call-return
                - Event-based
                - Repository
        - Allocation (Development, deployment and execution views of the architecture)
            - Addresses how the elements of the system are allocated to infrastructure and work teams;
            - Map elements to hardware and work teams;
            - Styles used when creating allocation views:
                - Deployment
                - Install
                - Work assignment

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

## Observations
- Always have the phase Iteration 0 in your project. This is where architectural design is built;
- A structure is architectural if it supports reasoning about the system and its properties;
    - The architecture needs to contain only portions of the system that are architecturally significant;
        - The architect should not design every single portion of the system. They have to understand the problem area and identify where the solution should fit within the organization;
        - Design only enough for the team to begin coding or to perform detailed design;
- Design choices that focus on implementation are non-architectural;
- Create prototypes for validating design concepts. It is often a tool for the more risky and lesser understood parts of the solution;
- Always set time constraints;
- An ideal design is attained not when there is no longer anything to add, but when there is no longer anything to take away.
- All approaches to design include 3 aspects that may be compared:
    - Design method - Systematic series of steps that the team uses to solve a problem; A sugestion of how to view the problem;
        - Object oriented design
        - Structured design
        - Role based design
    - Design representation
    - How that design is going to be validated;

## Books
- Software Architecture in Practice (3rd Edition)
- Documenting Software Architectures: Views and Beyond (2nd Edition)
