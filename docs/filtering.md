**Important note:** This should not be used by plugins/addons, instead they should do all their work in their own middleware.

**Deprecated:** _4.x.x_ doesn't support filtering anymore.

Before and after filters are evaluated before and after each request within the same context as the routes. They can modify the request and response.

The current filter supports all of the verbs which are RESTful, for example defining a before get filter looks like this:

```ruby
class DemoFilter < Grip::Controllers::Filter
  def call(context)
    context
      .json("Hello, World!")
  end
end

class Application < Grip::Application
  def routes
    filter :before, :get, "/", DemoFilter
  end
end
```

defining an after post filter looks like this:

```ruby
class DemoFilter < Grip::Controllers::Filter
  def call(context)
    context
      .json("Hello, World!")
  end
end

class Application < Grip::Application
  def routes
    filter :after, :post, "/", DemoFilter
  end
end
```
