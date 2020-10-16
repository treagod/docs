## Heroku

You can use [heroku-buildpack-crystal](https://github.com/crystal-lang/heroku-buildpack-crystal) to deploy your Grip application to Heroku.

## Cross Compilation

Cross-compilation is supported and it can be achieved using [this guide](http://crystal-lang.org/docs/syntax_and_semantics/cross-compilation.html)

## Environment

Grip respects the development/production flags, It is set to none by default.

To change this value to production, for example, use:

```bash
crystal run ./src/application.cr -Dproduction
```

To change this value to development, for example, use:

```bash
crystal run ./src/application.cr -Ddevelopment
```
