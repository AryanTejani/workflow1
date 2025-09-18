# Team Management Flow Diagram

```mermaid
graph TD

    subgraph Main User Flow
        A[User Navigates to Teams Tab] --> B{Is user in multiple teams?};
        B -- Yes --> C[Display Team Switcher Dropdown];
        B -- No --> D[Display Current Team Details];
        C --> D;
        D --> E[View Team Members];
    end

    subgraph Admin Actions
        E --> F{User is Admin?};
        F -- Yes --> G[Show Admin Controls];
        G --> H(Invite Member);
        G --> I(Edit Member);
        G --> J(Remove Member);
        G --> K(Transfer Ownership);
    end

    subgraph Invite Flow
        H --> L[Open Invite Modal];
        L --> M[Admin enters Email & optional Name];
        M --> N{User Exists?};
        N -- No --> O[Create New User in DB];
        N -- Yes --> P[Proceed];
        O --> P;
        P --> Q{Already a Member?};
        Q -- Yes --> R[Show Error Toast];
        Q -- No --> S[Create Invitation in DB];
        S --> T[Send Magic Link Email to Invitee];
    end

    subgraph Management Safeguards
        J --> J1[Confirm Removal];
        J1 --> J2{Is this the last admin?};
        J2 -- Yes --> J3[Block Action & Show Error];
        J2 -- No --> J4[Remove Member from DB];
        
        K --> K1[Confirm Transfer];
        K1 --> K2[Promote New User to Admin];
        K2 --> K3[Demote Old Admin to Regular];
    end
