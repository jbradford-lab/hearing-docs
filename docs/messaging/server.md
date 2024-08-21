---
sidebar_position: 2
---

# Server Messages

Messages from the server to the client take the following form:

```typescript
type Message = {
    type: "internal" | "error",
    message: string,
    [key: string]: any
}
```

## Internal Messages
These messages are received from the server in relation to the flow of a trial. These do not need to be displayed to the user and can be safely handled behind the scenes.

Internal messages that are currently being sent by the server include the following:

### `connected_to_server`
A confirmation message that the connection attempt was successful.

| Parameter | Type | Description |
|-----------|------|-------------|
| `date`    | String | Date the server was connected at (`toLocaleString()`)

### `session_created`
Confirmation that the session has been created

| Parameter | Type | Description |
|-----------|------|-------------|
| `device`  | UUID | The allocated device UUID |
| `sessionNo` | Number | The index of the current session |
| `repeat` | Number | The repeat the session is up to |
| `code` | Number | The 6-digit session join code |
| `studyMetadata` | Study | The data for this session |

### `session_continuing`
A current session already exists for this participant and must be continued.

| Parameter | Type | Description |
|-----------|------|-------------|
| `device`  | UUID | The allocated device UUID |
| `studyMetadata` | Study | The data for the study |
| `...` | [ActiveSession](./activeSession) | The full details of the current active session |

### `session_join`
The user has now joined the session successfully.

| Parameter | Type | Description |
|-----------|------|-------------|
| `device`  | UUID | The allocated device UUID |
| `sessionNo` | Number | The index of the current session |
| `repeat` | Number | What repeat the trial is up to |
| `studyMetadata` | Object | Contains the full details of the study |
| `isPrimary` | Boolean | Whether the device is the primary device |
| `joinCode` | Number | The session join code that was originally used |

### `session_update`

A message containing the latest details of the active session. Sent whenever a device joins or leaves the session. Designed to provide some way for the client to check what the current condition of the session is and if any action needs to be taken (e.g. as a result of there not being enough devices to continue with a trial).

| Parameter | Type | Description |
|-----------|------|-------------|
| `...`     | [ActiveSession](./activeSession) | The ActiveSession in the application |

### `trial_state_change`

Forwarding from the client whenever the state of the trial changes. Note that one of the following two parameters will be received, and it is imperative to check which.

| Parameter | Type | Description |
|-----------|------|-------------|
| `trial_metadata` | Object | The trial metadata as stored in the study data |
| `state_data` | Object | The state data as received from the client. |

:::note
For future reference, it may be better to have a separate message for the trial_metadata as this is used when a trial begins. It may just be a more clean way to track which of these parameters to be on the lookout for.
:::

### `trial_continue`

Forwarding a message from the client, indicating now is the time to continue with a previous trial that may have been lost due to some disconnection.

| Parameter | Type | Description |
|-----------|------|-------------|
| `trial_metadata` | Object | The trial metadata as stored in the study data |

### `trial_finishing`

Once the client indicates the trial is ready to be finished, send this message to the clients and expect results to be sent through.

No parameters are to be expected for this message.

### `trial_finished`

All results have been received by the server. Can now move to the next step.

No parameters are to be expected for this message.

### `session_finished`

There are no more trials to be completed. Therefore, the session is now complete.

No parameters are to be expected for this message.

### `study_finished`

The study has now been fully completed. There are no further trials to undertake.

No parameters are to be expected for this message.

### `lost_primary`

:::info

This server message has been removed in favour of the client determining whether a primary device is present from the `session_update` message. This is to make it easier handling the situation when there are less devices than required in a session AND the primary device has been disconnected. This responsibility is now for the client to manage.

:::

## Error Messages
There are several different error messages that are written into the system that can be thrown. Usually, these are in response to some data missing from a request from the client. However, there may be some instances when these messages are caused by some internal error (e.g. data loss).

These are labelled as `error` messages so that they may be displayed clearly during client-side development and resolved. Recommended to show a proper alert dialog when one of these messages is received from the server so as to prevent any further frustrations from a misbehaving system.

