```mermaid
graph LR
    subgraph Processes
        A((1.0 Authenticate Student))
        B((2.0 Deliver Exam))
        C((3.0 Accept & Grade Answers))
        D((4.0 Generate Result & Feedback))
    end

    subgraph Data Stores
        D1([D1 - Student Records])
        D2([D2 - Question Bank])
        D3([D3 - Exam Attempts / Responses])
        D4([D4 - Results Archive])
    end

    E[Student]

    %% External Entity (Student) to System Flows
    E -- Login Credentials --> A
    E -- Exam Request / token --> B
    B -- Questions / Timer --> E
    E -- Submitted Answers --> C
    D -- Result / Feedback --> E

    %% Process 1.0 (Authenticate) and D1
    A -- Validate Data --> D1
    D1 -- Fetch Student Record --> A

    %% Process 2.0 (Deliver) and D2
    B -- Fetch Questions / Setup --> D2
    D2 -- Exam Setup Data --> B

    %% Process 3.0 (Grade) and D2/D3
    C -- Compare to Correct Answers --> D2
    D2 -- Correct Answers --> C
    C -- Save Attempt / Responses --> D3

    %% Inter-Process Flow (3.0 to 4.0)
    C -- Raw Scores / Grades --> D

    %% Process 4.0 (Generate Result) and D4
    D -- Save Final Result --> D4
