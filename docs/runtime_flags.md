# Logging and persistence flags

1.Flag which outputs the events to a STDOUT as a text based log:

```bash
# -D is used to define a compile time flag.
crystal run ./src/application.cr -D verbose
```

# Configuration flags

1.Flag which strips down non-crucial parts of the framework:

```bash
# -D is used to define a compile time flag.
crystal run ./src/appliaction.cr -D minimal
```

2.Flag which strips down non-crucial parts of the framework and leaves the logging in place:

```bash
# -D is used to define a compile time flag.
crystal run ./src/appliaction.cr -D minimal_with_logs
```

3.Flag which strips down non-crucial parts of the framework:

```bash
# -D is used to define a compile time flag.
crystal run ./src/appliaction.cr -D logs
```

4.Flag which enables the Swagger UI support:

```bash
# -D is used to define a compile time flag.
crystal run ./src/appliaction.cr -D swagger
```

5.Flag which enables the Swagger UI support:

```bash
# -D is used to define a compile time flag.
crystal run ./src/appliaction.cr -D serveStatic
```

# Environment flags

1.Flag which switches the environment to testing:

```bash
# -D is used to define a compile time flag.
crystal run ./src/application.cr -D test
```

2.Flag which switches the environment to development:

```bash
# -D is used to define a compile time flag.
crystal run ./src/application.cr -D development
```

3.Flag which switches the environment to production:

```bash
# -D is used to define a compile time flag.
crystal run ./src/application.cr -D production
```
