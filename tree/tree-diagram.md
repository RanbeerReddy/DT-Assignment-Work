%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#e1f5fe', 'edgeLabelBackground':'#ffffff', 'tertiaryColor': '#fff'}}}%%
graph TD
    %% --- MAIN FLOW ---
    %% START node
    START([START<br/>The laptop is closed...])
    
    %% Axis 1: Locus (Victim vs Victor)
    subgraph Axis1 [Axis 1: Locus of Control]
        direction TB
        A1_Q1[A1_Q1<br/>Thinking of one task... Story?]
        A1_Q2[A1_Q2<br/>Driver or Passenger?]
        A1_Q3[A1_Q3<br/>After a setback, what focus?]
        A1_D1{A1_D1<br/>Decision<br/>Calculated on State}
        
        %% Adaptive tie-breaker branch for Axis 1
        A1_ADAPTIVE[A1_ADAPTIVE<br/>If rewind to 9 AM, change?]
        A1_D2{A1_D2<br/>Decision<br/>Final Resolve}
        
        %% Outcome reflections for Axis 1
        A1_REF_INT[[A1_REF_INT<br/>Reflection: Victor<br/>Growth Mindset]]
        A1_REF_EXT[[A1_REF_EXT<br/>Reflection: Victim<br/>External Focus]]
        
        BRIDGE_1_2(BRIDGE_1_2<br/>Transition to Contribution)
    end

    %% Axis 2: Orientation (Contribution vs Entitlement)
    subgraph Axis2 [Axis 2: Orientation]
        direction TB
        A2_Q1[A2_Q1<br/>Did you go above official list?]
        A2_Q2[A2_Q2<br/>Finished task: help or notice?]
        A2_D1{A2_D1<br/>Decision<br/>Calculated on State}
        
        %% Deep Adaptive branch for Axis 2 (Two questions)
        A2_ADAPTIVE[A2_ADAPTIVE<br/>Drowning colleague: Op or Inconvenience?]
        A2_ADAPTIVE1[A2_ADAPTIVE1<br/>Tight situation: Team or Fair?]
        A2_D2{A2_D2<br/>Decision<br/>Final Resolve}
        
        %% Outcome reflections for Axis 2
        A2_REF_CONTRIB[[A2_REF_CONTRIB<br/>Reflection: Contribution<br/>Value Surplus]]
        A2_REF_ENT[[A2_REF_ENT<br/>Reflection: Entitlement<br/>Self-Preservation]]
        
        BRIDGE_2_3(BRIDGE_2_3<br/>Transition to Impact)
    end

    %% Axis 3: Radius (Self vs Others)
    subgraph Axis3 [Axis 3: Radius of Concern]
        direction TB
        A3_Q1[A3_Q1<br/>Making decisions: what mattered?]
        A3_Q2[A3_Q2<br/>Stress: who were you worried about?]
        A3_D1{A3_D1<br/>Decision<br/>Calculated on State}
        
        %% Deep Adaptive branch for Axis 3 (Two questions)
        A3_ADAPTIVE[A3_ADAPTIVE<br/>Rewind: whose outcome mattered?]
        A3_ADAPTIVE1[A3_ADAPTIVE1<br/>Important person interaction: Presence?]
        A3_D2{A3_D2<br/>Decision<br/>Final Resolve}
        
        %% Outcome reflections for Axis 3
        A3_REF_OTHERS[[A3_REF_OTHERS<br/>Reflection: Others<br/>Self-Transcendence]]
        A3_REF_SELF[[A3_REF_SELF<br/>Reflection: Self<br/>Narrow Focus]]
    end

    SUMMARY[[SUMMARY<br/>Interpolated synthesis of dominant signals]]
    END([END<br/>Reflection Complete])

    %% --- LOGIC AND CONNECTIONS ---
    
    START --> A1_Q1
    A1_Q1 --> A1_Q2
    A1_Q2 --> A1_Q3
    A1_Q3 --> A1_D1
    
    %% Axis 1 Decision 1 Logic
    A1_D1 -- "axis1.internal > axis1.external" --> A1_REF_INT
    A1_D1 -- "axis1.external > axis1.internal" --> A1_REF_EXT
    A1_D1 -- "otherwise (Mixed/Tie)" --> A1_ADAPTIVE
    
    %% Axis 1 Adaptive path
    A1_ADAPTIVE --> A1_D2
    
    %% Axis 1 Decision 2 Logic (Final Resolve)
    A1_D2 -- "axis1.internal >= axis1.external" --> A1_REF_INT
    A1_D2 -- "axis1.external > axis1.internal" --> A1_REF_EXT
    
    A1_REF_INT --> BRIDGE_1_2
    A1_REF_EXT --> BRIDGE_1_2
    BRIDGE_1_2 --> A2_Q1
    
    %% Axis 2 Connections
    A2_Q1 --> A2_Q2
    A2_Q2 --> A2_D1
    
    %% Axis 2 Decision 1 Logic
    A2_D1 -- "axis2.contribution > axis2.entitlement" --> A2_REF_CONTRIB
    A2_D1 -- "axis2.entitlement > axis2.contribution" --> A2_REF_ENT
    A2_D1 -- "otherwise (Mixed/Tie)" --> A2_ADAPTIVE
    
    %% Axis 2 Deep Adaptive path
    A2_ADAPTIVE --> A2_ADAPTIVE1
    A2_ADAPTIVE1 --> A2_D2
    
    %% Axis 2 Decision 2 Logic (Final Resolve)
    A2_D2 -- "axis2.contribution >= axis2.entitlement" --> A2_REF_CONTRIB
    A2_D2 -- "axis2.entitlement > axis2.contribution" --> A2_REF_ENT
    
    A2_REF_CONTRIB --> BRIDGE_2_3
    A2_REF_ENT --> BRIDGE_2_3
    BRIDGE_2_3 --> A3_Q1
    
    %% Axis 3 Connections
    A3_Q1 --> A3_Q2
    A3_Q2 --> A3_D1
    
    %% Axis 3 Decision 1 Logic
    A3_D1 -- "axis3.others > axis3.self" --> A3_REF_OTHERS
    A3_D1 -- "axis3.self > axis3.others" --> A3_REF_SELF
    A3_D1 -- "otherwise (Mixed/Tie)" --> A3_ADAPTIVE
    
    %% Axis 3 Deep Adaptive path
    A3_ADAPTIVE --> A3_ADAPTIVE1
    A3_ADAPTIVE1 --> A3_D2
    
    %% Axis 3 Decision 2 Logic (Final Resolve)
    A3_D2 -- "axis3.others >= axis3.self" --> A3_REF_OTHERS
    A3_D2 -- "axis3.self > axis3.others" --> A3_REF_SELF
    
    %% Final Convergence
    A3_REF_OTHERS --> SUMMARY
    A3_REF_SELF --> SUMMARY
    SUMMARY --> END

    %% --- STYLING ---
    classDef question fill:#e1f5fe,stroke:#01579b,stroke-width:1px;
    classDef decision fill:#cfd8dc,stroke:#263238,stroke-width:2px;
    classDef reflection fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px,rx:5,ry:5;
    classDef bridge fill:#f9fbe7,stroke:#33691e,stroke-width:1px,stroke-dasharray: 5 5;
    classDef summary fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    classDef boundary fill:#fdfdfd,stroke:#9e9e9e,stroke-width:1px,stroke-dasharray: 5 5;
    
    class START,END fill:#333,stroke:#000,color:#fff;
    class A1_Q1,A1_Q2,A1_Q3,A1_ADAPTIVE,A2_Q1,A2_Q2,A2_ADAPTIVE,A2_ADAPTIVE1,A3_Q1,A3_Q2,A3_ADAPTIVE,A3_ADAPTIVE1 question;
    class A1_D1,A1_D2,A2_D1,A2_D2,A3_D1,A3_D2 decision;
    class A1_REF_INT,A1_REF_EXT,A2_REF_CONTRIB,A2_REF_ENT,A3_REF_OTHERS,A3_REF_SELF reflection;
    class BRIDGE_1_2,BRIDGE_2_3 bridge;
    class SUMMARY summary;
    class Axis1,Axis2,Axis3 boundary;