## Heroku

You can use [heroku-buildpack-crystal](https://github.com/crystal-lang/heroku-buildpack-crystal) to deploy your Grip application to Heroku.

## Cross Compilation

Cross-compilation is supported and it can be achieved using [this guide](http://crystal-lang.org/docs/syntax_and_semantics/cross-compilation.html)

## Environment

Grip respects the APP_ENV environment variable and Grip.config.env. It is set to development by default.

To change this value to production, for example, use:

```bash
$ export APP_ENV=production
```

If you prefer to do this from within your application, use:

```ruby
Grip.config.env = "production"
```
