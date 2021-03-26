In Grip raw middlewares are mentioned as handlers, when creating a handler you include the `HTTP::Handler` module and define a call/1 function.

```ruby
class DemoHandler
  include HTTP::Handler

  def call(context : HTTP::Server::Context) : HTTP::Server::Context
    # Mutate the context and pass it on to the next handler.
  end
end

class Application < Grip::Application
  # These are inserted after the exception handler
  def custom_handlers
    [
      DemoHandler.new
    ]
  end

  # These are inserted before the exception handler
  def root_handlers
    [
      DemoHandler.new
    ]
  end
end
```
