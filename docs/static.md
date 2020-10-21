Static file handler gives you an abilty to serve static files to clients.

```ruby
class Application < Grip::Application
  def public_dir # The directory from which the files will be served
    "./public"
  end

  def fallthrough # This enables the fallthrough feature which moves the request on to the next handler if this the file is not found.
    false
  end

  def directory_listing # This enables directory listing for the static file handler
    true
  end
end
```

Make sure to compile using the runtime flag `serveStatic`:

```bash
crystal run ./src/application.cr -DserveStatic
```
