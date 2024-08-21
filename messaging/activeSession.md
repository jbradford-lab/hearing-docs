
# ActiveSessions

The system actively keeps track of the sessions currently in progress through keeping a list of ActiveSession objects. These are created and modified throughout the lifecycle of a session and are referred to and sent throughout the system when there are changes, such as when a device joins or leaves a session.

## Object Structure
Note: please refer to `types.ts` for the latest version.

```typescript title="server/types.ts"
export interface ActiveSession { 
    participantId: string,
    joinCode: number,
    devices: Device[],
    currentTrial: number,
    currentSession: number,
    currentRepeat: number,
    active: boolean,
    trialInProgress: boolean,
    startDate: Date,
    serverVersion: string,
    trialMetadata?: any
}

export interface Device {
    uuid: string,
    isPrimary: boolean,
    clientVersion: string
}
```
