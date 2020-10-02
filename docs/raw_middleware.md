**Important note: Using the raw middleware is not recommended since it is a global handler which most of the time is reserved for the core functionality.**

In Grip raw middlewares are mentioned as handlers, when creating a handler you include the `HTTP::Handler` module and define a call/1 function.

```ruby
class DemoHandler
  include HTTP::Handler

  def call(context)
    # Mutate the context and pass it on to the next handler.
  end
end

class Application < Grip::Application
  def initialize
    # Add the middleware to the central stack.
    Grip.config.add_handler DemoHandler.new
  end
end
```
