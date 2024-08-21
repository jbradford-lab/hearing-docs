
# Study Configuration File
This page aims to go into depth about the various configuration flags that are available to customise the study to the required needs.

## Configuration Parameters
- `sessionFrequency` - how often a participant would complete each session.
    - Must be one of: `daily`, `altdaily`, `weekly`, `altweekly`
    - If none is provided, there is no restriction on how long a participant must wait before going to the next session.
- `repeatableAtCompletion` - can a session be repeated as soon as a participant has completed it (true or false)
- `repeatableAfterTTL` - can a session be repeated after having been completed but before the TTL has elapsed or the next session must begin (true or false).
- `minDevices` - The **minimum** number of devices that must be connected to a session before it can commence.
- `timeToLive` - How long a session can survive for before it is marked as inactive (measured in seconds).
- `sessions` - An array of the [sessions](/config/sessions) that must be conducted within the study. **Further details coming soon.**

## Default Configuration File
```json
{
    "id": 0,
    "name": "General Study",
    "sessionFrequency": "daily",
    "repeatableAtCompletion": true,
    "repeatableAfterTTL": false,
    "minDevices": 2,
    "timeToLive": 3600,
    "sessions": []
}
```
