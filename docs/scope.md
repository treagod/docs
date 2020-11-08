Scope defines a prefix for routes which will be nested in a block.

```ruby
class DemoController < Grip::Controllers::Http
  def get(context : Context) : Context
    context
      .json(nil)
  end
end

class Application < Grip::Application
  def routes
    # The routing occurs via the `get` macro which instantiates the controller class and assigns a route
    # to the routing mechanism.
    #
    # `GET /api/v1/` -> CLIENT -> SERVER -> ROUTER -> ROUTE -> CONTROLLER -> get/1
    #
    # `GET /api/v1/users/` -> CLIENT -> SERVER -> ROUTER -> ROUTE -> CONTROLLER -> get/1
    # 
    scope "/api/v1" do
      get "/", DemoController

      scope "/users" do
        get "/", DemoController
      end
    end
  end
end
```
