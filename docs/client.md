
# Client-Side Development

The client-side of the application is designed to be fully customisable to the needs of any study. The client can even be removed and completely remade if necessary. The design of the server aims to support this, and can effectively be used to faciliate any trial; not just one designed to assess hearing.

Two clients have been developed to demonstrate varying functionalities. The first is described below and was specifically developed to facilitate hearing tests. The second one was designed to facilitate a completely separate trial of reaction speeds.

## Provided Client (`/client`)

A client has been provided that aims to replicate the functionality included in previous iterations of this project, including:

- Reference and adjustable pitch playback (and adjustment)
- Handling of device disconnections rendering the trial unable to be completed.

### Providing Participant Code

You can now pass the participant code to the client by passing in a `participantCode` search query to the URL, such as below:

```
http://localhost/?participantCode=asdf
```

### Flow of the Client

The following diagram provides a visual depiction of how the different panels in the client flow from one to another. Please note that this diagram does not depict disconnection panels, such as the `LostPrimaryPanel` and `LostDevicesPanel` as these can arise at any stage during the normal operation of the client-side.

![Client-side flowchart](/client_flow.svg)

### Missing Features

At the time of writing, the client side isn't entirely complete. there are a few areas where further polish is needed, such as the following:

- Displaying error messages from the server in a human readable manner
- Assurance of mobile responsiveness

## Alternate Client (`/client-alt`)

To demonstrate the modularity of clients for different types of trials with the server, a second client was developed (though closely mimicking the structure of the existing client) to demonstrate a completely separate type of trial.

This alternate client is designed to test a user's reaction speed and to record the data as such. Currently, this client is developed to only work with a single user, but can easily be expanded to allow other devices to interact with it and operate in different ways.

The important thing to note is that with both of these clients, messages are exchanged constantly between the client and server to keep track of the state of the trial. Study, session, and trial metadata is fed as necessary between both ends. Results for the study are also recorded in the dtabase as expected.

### Key Differences

- The alternate client introduces works with a `maxDevices` limit as set in the study data; in this case, it is set to 1.
- The client does not send state data to other devices as it currently works by itself.

