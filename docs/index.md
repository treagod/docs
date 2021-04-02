Grip is a microframework for building RESTful web applications. It is designed to be modular and easy to use, with the ability to scale up to the limits of the Crystal programming language. It offers extensibility and it has integrated middleware called "pipes" which alter the parts of the request/response context and pass it on to the actual endpoint. It has a router which somewhat resembles that of [Phoenix framework](https://github.com/phoenixframework/phoenix)'s router and most of all it is fast, peaking at [1,663,946](https://www.techempower.com/benchmarks/#section=data-r19&hw=ph&test=json&l=zdk8an-1r) requests/second for plain text response.

## Project structure

For example a project structure of a normal Grip application should look like this:

```
# In this example the project name is `Echo`
lib/                # Library
src/
    application.cr         # Entry file
    echo/                  # Business logic, database interaction, etc.
        ...
    echo_web/              # Web layer to interact with the business layer.
        views/             # Views directory
            ...
        controllers/       # Controllers directory
            ...
shards.yml                 # The package configuration file
```
