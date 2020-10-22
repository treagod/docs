# Logging and persistence flags

1.Flag which outputs the events to a STDOUT as a text based log:

```bash
# -D is used to define a compile time flag.
crystal run ./src/application.cr -D verbose
```

# Configuration flags

1.Flag which strips adds logging to the framework:

```bash
# -D is used to define a compile time flag.
crystal run ./src/appliaction.cr -D logs
```

2.Flag which enables the Swagger UI support:

```bash
# -D is used to define a compile time flag.
crystal run ./src/appliaction.cr -D swagger
```

3.Flag which enables the static file:

```bash
# -D is used to define a compile time flag.
crystal run ./src/appliaction.cr -D serveStatic
```

4.Flag which enables the WebSocket support:

```bash
# -D is used to define a compile time flag.
crystal run ./src/appliaction.cr -D websocket
```

# Environment flags

1.Flag which switches the environment to testing:

```bash
# -D is used to define a compile time flag.
crystal run ./src/application.cr -D test
```
