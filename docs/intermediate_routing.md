The routing mechanism is based on `Kemal` which uses the radix tree implementation to identify the URL patterns.

```ruby
class DemoController < Grip::Controllers::Http
  def index(context : Context) : Context
    context
      .json(nil)
  end
end

class Application < Grip::Application
  def custom : Array(HTTP::Handler)
    [] of HTTP::Handler
  end

  def root : Array(HTTP::Handler)
    [] of HTTP::Handler
  end

  def routes
    # The routing occurs via the `get` macro which instantiates the controller class and assigns a route
    # to the routing mechanism, the `as` keyword creates a Proc(Context, Context) and wraps it around
    # the index/1 function f the DemoController.
    get "/", DemoController, as: :index
  end
end
```
