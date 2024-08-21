---
sidebar_position: 1
---

# Client (UI) Messages

The client sends the server various messages describing events occurring on the front-end. Messages from the client take take the following shape.

```typescript
type Message = {
    message: string,
    [key: string]: any
}
```

## Acceptable Events and Parameters

The server requires different parameters depending on the event that is being messaged. The following table outlines the different events that the client can message the server regarding and the parameters required.

### `session_new`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `client_version` | String | True | The current version of the client |
| `participant` | String | True | The participant ID as stored in the database |
| `device_uuid` | UUID | False | The UUID of the device, if available |

### `session_join`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `client_version` | String | True | The current version of the client |
| `join_code` | Number | True | The 6-digit join code generated upon `session_created` being received. |
| `device_uuid` | UUID | False | The UUID of the device, if available |

### `trial_next`

No additional parameters are required for the `trial_next` event.

### `trial_continue`

No additional parameters are required for the `trial_continue` event.

### `trial_state_change`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `state_data` | Any | True | Any arbitrary state data to be sent to the client. |

### `trial_finishing`

No additional parameters are required for the `trial_finishing` event.

### `trial_results`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `results` | Any | True | Any arbitrary results to be stored in the database. |

### `trial_finished`

No additional parameters are required for the `trial_finished` event.

### `session_finished`

No additional parameters are required for the `session_finished` event.

:::info

Please note that this message is only intended to be used if the participant wishes to end the session early. The server decides when a session has ended as indicated by the `session_finished` message that it emits.

:::

