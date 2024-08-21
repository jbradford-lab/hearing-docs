
# Sessions Configuration

A study can contain any number of sessions. Each session has an id (representing its index, or position in the study) and a list of trials that the participant may complete. Each trial can contain any arbitrary data, which will be sent to the client upon the trial commencing.

## Configuration Parameters
- `id`: An integer value representing the index of the session in the study.
- `trials`: An array of objects contianing **any** data that will be sent to the client and stored in the database upon a trial commencing.

## An Example Session
```json
{
    "id": 0,
    "trials": [
        {
            "id": 0,
            "task": "arbitrary",
            "ref": 1234
        },
        {
            "id": 1,
            "task": "arbitrary",
            "ref": 5678
        }
    ]
}
```


