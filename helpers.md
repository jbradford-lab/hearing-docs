# Helper Scripts

The application server folder includes a couple of helper scripts that are designed to support basic operations with the application and the database. In future iterations, ideally a GUI would be developed that would faciliate this instead.

These scripts can be executed using: `npx ts-node <script-name>.ts`

## Available Scripts

### `add-participant.ts`

This script supports adding a participant to the database. It will ask you for the name of the participant and to enter a unique code that the participant will either enter or that will be incldued in their special link to access the application.

### `retrieve-participant-sessions.ts`

This script will retrieve all recorded sessions for the participant with a specified code and will store them in a JSON file at a specified path.

## Environment Variables

These scripts rely on the `.env` file in the same directory as the server so it knows where the MongoDB Database is. As long as this variable is specified, then the scripts should work as expected.
