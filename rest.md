
# REST Server

This application also provides a REST server (via Express.js) to assist with debugging, and potentially (though most unlikely) to also host the front-end.

## Server Endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| /        | GET    | To confirm the Express server is operational |
| /study   | GET    | To get the current details about the study   |
| /participants | GET    | To get the list of participants currently stored inside the database. |
