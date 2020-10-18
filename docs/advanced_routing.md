The more advanced the route is the more time it takes when executed, since the call to the index function is an indirect call, meaning that the `index/1` never existed in the `Grip::Controllers::Http` class it needs to be wrapped in a `Proc` which then needs to be called.

```ruby
class DemoController < Grip::Controllers::Http
  def index(context)
    context
      .json(nil)
  end
end

class Application < Grip::Application
  def routes
    pipeline :api, [
      Pipes::PoweredByHeader.new
    ]

    pipeline :web, [
      Pipes::SecureHeaders.new
    ]

    # The routing occurs via the `get` macro which instantiates the controller class and assigns a route
    # to the routing mechanism.
    #
    # `GET /` -> CLIENT -> SERVER -> ROUTER -> ROUTE -> PIPELINE -> CONTROLLER -> index/1
    #
    # You can route the request through unlimited amounts of pipelines.
    get "/", DemoController, override: :index, via: [:web, :api]
  end
end
```
