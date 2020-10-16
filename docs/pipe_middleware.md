Pipe middleware is the building block of the framework, some helpful pipes are included with the framework.

Creating a custom pipe is as easy as creating an `HTTP handler`:

```ruby
class DemoPipe < Grip::Pipes::Base
  def call(context)
    # Mutate the context and pass it on to the next handler.
  end
end

class DemoController < Grip::Controllers::Http
  def get(context)
    context
      .json("Hello, World!")
  end
end

class Application < Grip::Application
  def routes
    # Creating a pipeline with a single pipe to be routed through.
    pipeline :web, [
      DemoPipe.new
    ]

    get "/", DemoController, via: :web
  end
end
```

Advantage of the pipe over a raw middleware is that you can controll which routes go through the middleware and which don't.
