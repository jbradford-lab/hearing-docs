
# Starting vs Continuing Logic

The below flowchart describes the logic that was implemented to determine whether to start a new session or continue an existing one given a user requests to start a new session.

```mermaid
flowchart TD
    start(Start a Session)
    isPresent{ }
    isEmpty{ }
    isEarly{ }
    start-->isPresent
    isPresent--Session present-->isEmpty
    isPresent--No session present-->isEarly
    isEmpty--Not empty-->inProgress(Already in progress)
    isEmpty--Is empty-->isExpired{ }
    isExpired--Not expired-->continue(Continue session)
    isExpired--Expired (TTL)-->inactive(Mark as inactive)
    inactive-->canRepeat{ }
    canRepeat--Can repeat-->createRepeat(Create repeat session)-->returnSession(Return session code)
    canRepeat--Cannot repeat-->isEarly
    isEarly--Too early-->cannotStart(Cannot start new session)
    isEarly--Not too early-->createSession(Create new session)-->returnSession
```

## Assumptions
- That the user can repeat a session if they have not passed the specified Time To Live (TTL) for that study, provided that is allowed through the `isRepeatable` flag.
- That if the user is to continue an existing session, that they are **not** provided with the join code.

