# Application Design

## Index
1. [Presentation Layer](#presentation_layer)


## <a name="presentation_layer"></a>1. Presentation Layer

Implements functionallity required to allow users to interact with the application. Two parts comprise this layer;

### 1.1 User Interface Components

These are visual components used to display info to user and accept input.

**ps:** UI components designed to work in a **separated presentation pattern implementation** are sometimes called **Views**.

--

### 1.2 Presentation Logic Components:

The code that defines the logical behavior and structure of the application in a way that is independent of any user interface implementation. Also responsible for organizing data from the business layer in consumable format for the UI components. This layer can be subdivided into two categories:

#### 1.2.1. Presenter, Controller, Presentation Model and ViewModel Components

Used when implementing the Separated Presentation pattern, these components encapsulate presentation logic within the presentation layer. To maximize reuse opportunities and testability, these components are not specific to any specific UI classes, elements, or controls.


#### 1.2.2. Presentation Entity Components

These components encapsulate business logic and data and make it easy for the UI and presentation logic components in the presentation layer to consume. E.g., performing data type conversion or aggregating data from several sources.

Presentation entities help to ensure data consistency and validity in the presentation layer. In some separated presentation patterns these components are sometimes referred to as models.
