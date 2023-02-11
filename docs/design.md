# Registration:

We are trying to go for a 3rd party registration pattern, as we want to
support all kinds of applications running on a server

Design is somewhat inspired from [Netflix Prana](https://github.com/Netflix/Prana).

librarian-c, though a side-car/daemon will be the main application when we start a VM/Container/Pod. This will give controller to when the main application launches and shutdowns.

We are looking at below features:

- register with librarian when application starts
- de-register when application shuts down gracefully or suddenly
- de-register when application health is down and re-register back application is up and running

For this we are going to let librarian-d start the main process and keep a handle on.

Another other daemons running like agents/splunkd/logging service daemon/webauthd/ etc needs to handle their own lifecycle via signals. Right now we are not thinking
of other side cars (maybe in future it handles everything - should be simple)

# Discovery:

The client itself is not librarian-d right now. This is where it differs from Prana.
librarian can send back response in xml/json/proto over REST api when requested for
all running instances for a service.

This being a client-side discovery, the client makes a call and makes a call to the
respective service.

librarian is a just a server and provides the locations in which the requested service is running.

# Distributed:

Right now we are thinking of a true cloud native architecture, and librarian is a single point of failure. Since this is an education project, we do this stuff when its time and not right now; so in future depending on how we do distributed we might have to redesign.

# Database:

Right now all information will be stored in a sql based server. Even if we do distributed, we might have an option to switch over to cockroach db.

**NOTE**: All design decisions are taken on basis of what I know right now, what I can achieve and my learning !!!!
